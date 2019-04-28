# DoodleNet

This is a series of experiments I did about Doodle Classifier(Convolutional neural network) using tensorflow.js and tensorflow. The data I used is from [Quickdraw dataset](https://quickdraw.withgoogle.com/data).

Here are a list of the projects - 
1. Train a doodle classifier in the browser with [tf.js](https://www.tensorflow.org/js/)
2. Train a doodle classifier with 345 classes with tensorflow, and port it to tf.js in the browser
3. KNN doodle classifier: Customizable doodle classes

Checkout Machine Learning for the Web [Week 3](https://github.com/yining1023/machine-learning-for-the-web/tree/master/week3-doodleclassifier) for more info and how does CNN and transfer learning work.

## 1. Train a doodle classifier in the browser with [tf.js](https://www.tensorflow.org/js/)
I trained a doodle classifier with 3 categories(bowtie, lollipop, rainbow) in the browser using tfjs' [layers API](https://github.com/tensorflow/tfjs-layers) and [tf.js-vis](https://github.com/tensorflow/tfjs-vis). The code is based on [tf.js Example - Training MNIST](https://github.com/tensorflow/tfjs-examples/tree/master/mnist).

<img src="https://raw.githubusercontent.com/yining1023/doodleNet/master/demo/tfjsdoodle.gif">

Try a live demo [here]().

Once you open the webpage, wait until the page load the data, train the model, evaluate the model. It will download two files: `myDoodleNet.json` and `myDoodleNet.weights.bin`. To test this model your self, you can load these two files back, and click on 'load model' button, then draw sth on the canvas, hit 'Guess' button to let model start guessing the drawing.

## 2. Train a doodle classifier with 345 classes with tensorflow, and port it to tf.js in the browser
It's trained on all 345 categories from Quickdraw dataset, 50k images per class. Here is the training [collab notebook](https://github.com/yining1023/doodleNet/blob/master/doodleNet.ipynb). ***This notebook is heavily based on [@zaidalyafeai](https://github.com/zaidalyafeai)'s Sketcher [notebook](https://github.com/zaidalyafeai/Notebooks) on 100 classes.*** I expanded the data to 345 classes and added a few layers to improve the accurary on 345 classes.

<img src="https://raw.githubusercontent.com/yining1023/doodleNet/master/demo/doodleNet.gif">

See a live demo [here](https://yining1023.github.io/doodleNet/demo)

Model Summary
```
Layer (type)                 Output Shape              Param #   
=================================================================
conv2d (Conv2D)              (None, 28, 28, 16)        160       
_________________________________________________________________
conv2d_1 (Conv2D)            (None, 28, 28, 16)        2320      
_________________________________________________________________
max_pooling2d (MaxPooling2D) (None, 14, 14, 16)        0         
_________________________________________________________________
conv2d_2 (Conv2D)            (None, 14, 14, 32)        4640      
_________________________________________________________________
conv2d_3 (Conv2D)            (None, 14, 14, 32)        9248      
_________________________________________________________________
max_pooling2d_1 (MaxPooling2 (None, 7, 7, 32)          0         
_________________________________________________________________
conv2d_4 (Conv2D)            (None, 7, 7, 64)          18496     
_________________________________________________________________
conv2d_5 (Conv2D)            (None, 7, 7, 64)          36928     
_________________________________________________________________
max_pooling2d_2 (MaxPooling2 (None, 3, 3, 64)          0         
_________________________________________________________________
flatten (Flatten)            (None, 576)               0         
_________________________________________________________________
dropout (Dropout)            (None, 576)               0         
_________________________________________________________________
dense (Dense)                (None, 512)               295424    
_________________________________________________________________
dense_1 (Dense)              (None, 345)               176985    
=================================================================
Total params: 544,201
Trainable params: 544,201
Non-trainable params: 0
_________________________________________________________________
None
```

## 3. KNN doodle classifier: Customizable doodle classes
Based on the previous doodle classifier of 345 classes, I added KNN classifier to it, so people can customize their own doodle classes.

<img src="https://raw.githubusercontent.com/yining1023/doodleNet/master/demo/tfjsdoodle.gif">

Try a live demo [here]().

You can draw 10+ circles and add them to class A, and draw 10+ lines and add them to class B, then let the model to guess your new drawing. You can define any other classes, it doesn't need to be circles or lines.
