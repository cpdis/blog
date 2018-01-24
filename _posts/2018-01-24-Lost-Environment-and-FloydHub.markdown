---
title: Lost Environment and FloyHub
layout: post
date: 2018-01-24 15:32:35 -0600
image: /assets/images/
headerImage: False
tag:
- python
- anaconda
- floydhub
- yearofml
star: False
category: blog
author: cpdis
description: Discussing how I lost my Anaconda machine learning environment and discovery of FloyHub.
---

It turns out that at some point in the past few months the environment that I had setup for machine learning ([Tensorflow](https://www.tensorflow.org), [Keras](https://keras.io), [OpenCV](http://opencv-python-tutroals.readthedocs.io/en/latest/), etc.) was somehow lost in the ether. 

How could this happen you might ask? I used [Anaconda](https://www.anaconda.com) to manage the different environments I had (`source activate myenv` and `source deactivate myenv`) and I recently did a clean install of Python to clear up some issues I was having with regard to [Udacity’s Self Driving Car Nanodegree](https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013). Because of this, when I went to start on the project for this week, [Breaking a CAPTCHA in 15 minutes](https://medium.com/@ageitgey/how-to-break-a-captcha-system-in-15-minutes-with-machine-learning-dbebb035a710), I realized that none of the packages I had previously installed were there. Not good. Fortunately, I like starting things from scratch and this gives me the opportunity to write a post about the way that I setup my environment.

While I was researching how different people have set up their machine learning environments I came across FloydHub. FloydHub is one of the newish class of platform-as-a-service (PaaS) services. They basically allow you to train and deploy deep learning models in the cloud with just a few commands and parameters on the command line. Most of the popular frameworks are available (`floyd run --env tensorflow`) and a range of hardware is available at relatively affordable prices at per second rates. 

One of the highlights of FloydHub (setting aside making the whole process almost frictionless) is the ability to create a Jupyter notebook for the project when you’re starting your model. Follow along and see how easy it is to get a model running:

### 1. Create a FloydHub account

* [Sign up](https://www.floydhub.com/signup) on FloydHub
* Install the floyd CLI on your local machine through these two [steps](https://www.floydhub.com/welcome):

```
$ pip install -U floyd-cli

$ floyd login
# Follow the instructions on your CLI
```

Upon logging in, you will need to copy and paste a private key into the command line that authenticates your machine with the service. FloydHub provides a nice UX for copying that 🔑 during the account creation process—it’s the little things that make you like a product.

### 2. Clone this project to your local machine

```
$ cd /path/to/your-project-dir
$ floyd clone experiments/
```

### 3. Create your project version on FloydHub
* [Create a project](https://www.floydhub.com/projects/create) on FloydHub and then sync the cloned repository with your new project:

`$ floyd init your-project-name`

### 4. Run the project through a jupyter notebook

* The `--env` flag specifies the environment that this project should run on.
* The `--data` flag specifies the dataset that should be available in the `/data` directory and the models should be available at the `/models` directory
* The `--mode` flag specifies that the job should create a Jupyter notebook.
* The `--gpu` flag specifies whether the GPU should be used to accelerate the training process.

```
floyd run \
  --env tensorflow:py2 \
  --data experiments/datasets/🐶/2:data \
  --data experiments/datasets/🐶-models/1:models \
  --mode jupyter \
  --gpu
```

Once the job is started, the jupyter notebook will open in your browser and you are ready to go!

The next post will be about setting up my machine learning environment followed by the project that I was tentatively supposed to be finished with a few days ago.

