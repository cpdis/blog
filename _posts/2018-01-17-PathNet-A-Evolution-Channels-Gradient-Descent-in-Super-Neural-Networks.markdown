---
title: PathNet - Evolution Channels Gradient Descent in Super Neural Networks
layout: post
date: 2018-01-17 13:40:10 -0600
image: /assets/images/
headerImage: False
tag:
- transfer learning
- evolution learning
- continual learning
- giant networks 
- yearofml
star: False
category: blog
author: cpdis
description: New deep learning architecture that combines modular deep learning, meta-learning, and reinforcement learning.
---

*Note: Inevitably, this past week was much more busy than planned. As such, I didn’t get to explore much more than the paper itself and the Github repository. I’d rather not do the minimum amount of work to achieve a goal but in this case it’s the best I can do.*

I first came across PathNet in Azeem Azhar’s essential [The Exponential View](https://www.getrevue.co/profile/azeem?utm_campaign=Issue&utm_content=forwarded&utm_medium=email&utm_source=Azeem+Azhar%3A+The+Exponential+View) newsletter almost exactly a year ago. DeepMind was causing a stir in the AI community because PathNet was a plausible precursor to an architecture that could support artificial general intelligence (AGI). PathNet combines modular deep learning, meta-learning, and reinforcement learning and is summarized this way in the introduction to the [paper](https://arxiv.org/abs/1701.08734):
> For artificial general intelligence (AGI) it would be efficient if multiple users trained the same giant neural network, permitting parameter reuse, without catastrophic forgetting. PathNet is a first step in this direction. It is a neural network algorithm that uses agents embedded in the neural network whose task is to discover which parts of the network to re-use for new tasks.  

Neural networks, in general, are trained on data for each specific task they are trying to achieve. This is time consuming and not efficient. Transfer learning was developed to bypass this problem but has limited use. PathNet goes beyond transfer learning, where knowledge gained while solving one problem is applied to a different but related problem, it finds the best parameters to be reused for transfer learning and implements those. Essentially, a neural network of neural networks. 

A PathNet is a modular deep neural network with any number of layers consisting of modules. Each module within each layer is itself a neural network (see last sentence of the previous paragraph). Each neural network module is either convolutional or linear and is followed by a transfer function (RELUs in this case). At each layer the output of each module is summed and then passed on to the next layer. While there may be an arbitrary number of modules per layer, typically a maximum of 3 or 4 distinct modules are permitted in the final pathway. The final layer in a PathNet is unique and not shared between different tasks. The figure belows shows this model in action. The first three layers are convolutional 2D kernels with 8 kernels per module (the green boxes in the figure), kernel sizes of (8, 4, 3), and strides (4, 2, 1) from the first to the third layer, respectively. After each module is a RELU and the layers are summed before being passed on to the next layer (light blue boxes). The red boxes show the modules that are passed on to the next layer, if all modules were included then as the model evolved it would simply grow to encompass the entire network.

![Atari](/assets/images/16-01-18/atari.jpeg)

The tasks that were considered were MNIST classification, CIFAR and SVHN, several Atari games, and several Labyrinth games. For binary MNIST classification the researchers found that PathNet helped speed up learning in the classification task by decreasing the mean time to solution from 229 generations to 167 generations. They found this to be the case for both the control (independent learning) and when the hyperparameters were fine tuned. The speedup ratio compared to independent learning was 1.18. The histograms below clearly show the reduction in the number of generations to achieve 0.998 accuracy. 

![MNIST](/assets/images/16-01-18/MNIST.jpeg)

Moving on to the Atari games, the researchers found that PathNet was superior to fine-tuning. fine-tuning was performed by doing a hyperparameter sweep of learning rates and entropy costs while PathNet was investigated using a range of evaluation times, mutation rates, and tournament sizes. [I understand that it's necessary to tune the model to achieve optimal results, however, if you must tune PathNet doesn't that make it a little less viable as AGI?] An optimal combination of tournament size and mutation rate were found for PathNet that achieved rapid convergence and a speedup ratio of 1.33 versus 1.16 for fine-tuning. The figure below shows the results for the first 40 million steps of training for PathNet (blue), fine-tuning (green), and independent learning (red). The results for both PathNet and fine-tuning show the top five hyperparameter settings.

![Atari2](/assets/images/Atari2/atari2.jpeg)

Finally, three labyrinth games were tested, `lt_chasm`, `seekavoid_arena`, and `stairway_to_melon`. All of the games are part of DeepMind's [DeepMind Lab](https://github.com/deepmind/lab). Again, a hyperparameter sweep was used for fine-tuning; mutation rates, module duplication rates, and tournament size were varied while learning rate, entropy cost, and evaluation time were fixed. PathNet learns the second task faster than fine tuning for transfer to `lt_chasm` and transfer from `lt_chasm` to `seekavoid_arena`. PathNet also performs better when learning `stairway_to_melon` and `seekavoid_arena` from scratch. Interestingly, when transferring to `lt_chasm`, both fine tuning and PathNet perform worse than independent learning. Speedup for PathNet is 1.26 versus 1.0 for fine-tuning (this is skewed by the good performance of transferring from `seekavoid_arena` to `stairway_to_melon`). The figure below shows the mean of the five best training runes for PathNet compared with fine-tuning (the off diagonal plots) and independent learning (diagonal plots labeled from scratch). The results are more mixed than the previous examples, however, in most cases PathNet performs better than the control. especially when transferring from one game to another. 

![Labyrinth](/assets/images/16-01-18/labyrinth.jpeg)

It's pretty clear that PathNet represents a step toward AGI. I wish that I had more time to look at the [code](https://github.com/jaesik817/pathnet), play with it, and see it in action with some of the examples from the paper but I'm unfortunately already behind with this project. 

The code, notes, and reference files for this week are in this [repository](https://github.com/cpdis/Experiments/tree/master/1_DeepMind_PathNet).

