---
# Course title, summary, and position.
linktitle: ML Introduction
summary: Tutorial page for slides and midterm/exam review material.
weight: 1

# Page metadata.
title: Introduction To Machine Learning
date: "2018-09-09T00:00:00Z"
lastmod: "2018-09-09T00:00:00Z"
draft: false  # Is this a draft? true/false
toc: false  # Show table of contents? true/false
type: docs  # Do not modify.

# Add menu entry to sidebar.
# - name: Declare this menu item as a parent with ID `name`.
# - weight: Position of link in menu.
menu:
 ml_intro:
    name: ML Introduction
    weight: 1
---

This is an introductory tutorial on machine learning using the scikit-learn and Keras Python packages. Prerequisites are minimal; chiefly, I assume that the reader has a little bit of prior programming experience—preferably in Python. A passing familiarity with basic inferential statistical methods (primarily linear regression) is also helpful, but isn't essential. Some of the material in thi tutorial is borrowed from Jake Vanderplas's excellent <a href="https://github.com/jakevdp/sklearn_tutorial" target="_blank">scikit-learn tutorial</a>. The main differences between the present tutorial and most others out there are that (a) this tutorial is more verbose than most (i.e., the emphasis is on conceptual understanding rather than just on learning the scikit-learn API), and (b) most of the examples are drawn from more unique datasets and contain application to real world examples.

## Software

All of the code in this tutorial is written in Python. There is nothing intrinsically special about Python in the machine learning context; in principle, all of the examples and simulations in these pages could have been written in other languages (R, Matlab, etc.). Indeed, there are plenty of machine learning tutorials out there written in other languages.That said, Python does have a number of practical advantages over other languages. Chief among these is the fact that it's currently the most widely used language in the data science and machine learning community. This means there are exceptional tools written in Python for virtually every domain of machine learning. Exhibit A is the <a href="https://scikit-learn.org/stable/" target="_blank">scikit-learn</a> package for machine learning. Scikit-learn is the world's most widely used machine learning, and some of the reasons for its popularity will hopefully soon become clear. Scikit-learn is itself built on the <a href="https://www.numpy.org" target="_blank">numpy</a> numerical computing library, which we'll also use fairly regular. Exihbit B is the <a href="https://keras.io/" target="_blank">Keras</a> package for machine learning. Keras is a high-level neural networks API, written in Python and capable of running on top of <a href="https://github.com/tensorflow/tensorflow" target="_blank">TensorFlow</a>. It was developed with a focus on enabling fast experimentation.

## The scikit-learn package

Now that we know what machine learning is, let's turn to the scikit-learn package. Scikit-learn is the most widely-used machine learning package in Python (and probably the most widely-used ML package, period). Its popularity stems from its simple, elegant API, <a href="https://scikit-learn.org/stable/documentation.html" target="_blank">stellar documentation</a>, and comprehensive support for many of the most widely used machine learning algorithms (the main exception being deep learning, which we will use Keras for). Scikit-learn provides well-organized, high-quality tools for virtually all aspects of the typical machine learning workflow, including data loading and preprocessing, feature extraction and feature selection, dimensionality reduction, model selection and evaluation, and so on.

# Python Setup

First you will need to install Python, depending on what operating system you are using there are different approaches.

## Mac

1. Install Homebrew by opening a Terminal window and pasting the following line. 

```console
/usr/bin/ruby -e $(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)
```

2. Homebrew asks you to enter your password so it can finalize the installation. Enter your user account password and hit enter
3. Once Homebrew has finished installing, return to your terminal and run the following command:

```console
brew install python3
```

## Windows

1. You will need to download the <a href="https://www.python.org/downloads/windows/" target="_blank">windows python installer</a>.
2. Underneath the heading at the top that says Python Releases for Windows, click on the link for the Latest Python 3 Release - Python 3.x.x
3. Scroll to the bottom and select either Windows x86-64 executable installer for 64-bit or Windows x86 executable installer for 32-bit
4. Install by double-clicking on the downloaded file.

## Linux

1. Open a terminal window and run the following commands:

```console
sudo apt-get install python3.6
sudo apt install python3-pip
```

# Python Interactor

Several Python integrated development environments (IDE) exist to make writting Python code easier. The one I use the most, and I highly recommend, is Spyder IDE. Spyder is a powerful scientific environment written in Python, for Python, and designed by and for scientists, engineers and data analysts. It offers a unique combination of the advanced editing, analysis, debugging, and profiling functionality of a comprehensive development tool with the data exploration, interactive execution, deep inspection, and beautiful visualization capabilities of a scientific package.

Once you have installed Python, installing Spyder is straight forward. You will need to open a terminal or command prompt and type the following

```console
pip install spyder
```
