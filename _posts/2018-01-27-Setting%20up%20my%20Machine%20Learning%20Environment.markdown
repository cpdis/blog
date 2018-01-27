---
title: Setting up my Machine Learning Environment
layout: post
date: 2018-01-27 10:47:39 -0600
image: /assets/images/
headerImage: False
tag:
- machine learning
- Anaconda
- tensorflow
- keras
- yearofML
star: False
category: blog
author: cpdis
description:Install Anaconda, setup a conda environment, and install the required packages for deep learning.
---

As I mentioned in my last post, I unfortunately lost my machine learning environment that I had set up on my laptop. Fortunately, though, getting up and running with Python, Keras, and Tensorflow is quite easy. All of the individual packages that you might want to use for machine/deep learning can be downloaded, cloned, acquired individually but it seems like the standard (and easiest for beginners) method is to use a distribution like [Anaconda](https://www.continuum.io/downloads). 

Anaconda is a leading open data science platform that's powered by Python. I'll be using the open source version but there's also an [enterprise](https://www.anaconda.com/enterprise/) distribution as well. The major benefit of using a distribution is that out of the box it includes over 100 (read *most*) of the most popular Python and R packages for data science. 

## Creating a conda environment
Also included with Anaconda is a versatile package manager call `conda`. Like [Homebrew](https://brew.sh/), it quickly installs, runs, and updates packages and their dependencies. You can also use it to search the package index, create new environments (the main point of this post), and install packages into existing environments.

`conda` environments are collections of packages with specific versions that can be used to ensure the portability of Python code. This is useful when collaborating with someone or using two different versions of a package simultaneously. I created two machine learning environments, `ML2` and `ML3`. Based off of Python 2.7.14 and 3.6.4, respectively. It only took a few simple steps to create both of these environments.

In Terminal type:

```
conda create -n ML2 python=2.7.14 pandas scikit-learn jupyter matplotlib
```

and hit `Enter`. When prompted, answer `y` and you should see this:

```
# To activate this environment, use:
# > source activate ML2
#
# To deactivate this environment, use:
# > source deactivate ML2
```

Activating the environment is as simple as typing:

```
source activate ML2
```

You can see that the environment is activated because the name `(ML2)` is prepended to your prompt.

## Install Tensorflow and Keras
[TensorFlow](https://www.tensorflow.org/) is an open source software library for numerical computation using data flow graphs. The way that it is built allows it to be used on one or more CPUs, GPUs, servers, or phones with a single API. It was originally developed by researchers and engineers on the Google Brain Team. 

To install TensorFlow, make sure the environment you want to use is active, in this case `ML2` and type:

```
pip install tensorflow
```

The other super useful package is [Keras](https://keras.io/), a high-level neural network specification implemented in Python that runs on top of TensorFlow. It makes creating a model much simpler than using TensorFlow which is paramount for fast experimentation.

To install Keras, make sure the environment you want to use is active, in this case `ML2` and type:

```
pip install keras
```

## Test it!

To make sure everything is running smoothly type:

```
ipython
```

which will bring up the iPython console and display:

```
Python 2.7.13 |Continuum Analytics, Inc.| (default, Dec 20 2016, 23:05:08) 
Type "copyright", "credits" or "license" for more information.

IPython 5.3.0 -- An enhanced Interactive Python.
?         -> Introduction and overview of IPython's features.
%quickref -> Quick reference.
help      -> Python's own help system.
object?   -> Details about 'object', use 'object??' for extra details. details.

In [1]:
```

Import TensorFlow and Keras:

```
import tensorflow, keras
```

which should result in the following output:

```
Using TensorFlow backend.
```

These aren’t the only tools that I’ll be using but they are a solid base. Distributions such as Anaconda and package managers like conda, pip, and homebrew make adding new tools extremely easy.

