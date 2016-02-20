CIFAR10 Convolutional Neural Network
==========

This is a convolutional neural network in python.
The code is an ipython notebook (if you are on github you can probably even view it online). Libraries used are Fuel, Theano and Lasagne. 
This is an experiment for the Neural Network course at Wroclaw University:

https://sites.google.com/a/cs.uni.wroc.pl/jch/teaching/neuralnetworks15

Data
----------
Test data is a set of 60 000 32x32 color images called CIFAR10.
Training data (50 000 samples) is split into two sets:
* training set (images 1 - 40 000)
* validation set (images 40 001 - 50 000)
Test data consists of remaining 10 000 samples.

Currently the network achieves around 80% accuracy. 

Preprocessing done on the data - scaling of data from color channels with results saved into 32-bit float numbers.

Layers used: 
----------
* Convolutional layers with linear rectifier
* 2D MaxPool layers
* Dropout layer
* Softmax layer

Network architecture:
----------
* Convolutional layer with 128 units of 5x5 filter size
* Rectifier
* Max Pooling with (2,2) pool size
* Convolutional layer with 256 units of 5x5 filter size
* Rectifier
* Max Pooling with (2,2) pool size
* Convolutional layer with 512 units of 3x3 filter size
* Rectifier
* Convolutional layer with 1024 units of 2x2 filter size
* Rectifier
* Dropout with probabiliy 50%
* Softmax 

Techniques
----------
The data is loaded, split into sets and preprocessed.
Then the network is build and compiled into machine code for current
architecture.
After that the network parametrs are initialized and it is trained with 
Stochastic Gradient Descent for a number of rounds (depending on the loss
from previous rounds). Training data is reordered between the rounds.
After each round mean loss and validation accuracy is computed for the training
and the validation set (and printed out). Finally network accuracy is tested
on the test data, network parameters can be saved and the output is logged.

Fuel library makes data management easy.
I used it to load the data, rescale it and divide it into batches.
Fuel data streams helped to randomly reorder data samples in training.

Theano made efficient GPU computations possible without having to write 
a single line of CUDA code. The speedup after moving from a fast CPU to
a top-of-the-shelf GPU was 60 times. Wow.

Lasange was used to build the network. Layer implementations, training
algorithm, loss functions, regularization, connecting layers, parameters
saving and loading, all that is provided by Lasagne. 

Files:
----------
* convnet.ipynb - source code
* params.bin - parameters of a trained network
* restuls - results on the test set. Format: classifier_output real_label 

Current problems:
----------
* Architecture of this network renders training on CPUs rather infeasible (long computations).
* Overfitting - network tends to fit to the training data too closely, sacraficing generality and resulting worse on the validation and test sets. I tried implementing some sort of regularization to overcome the problem but apparently it is implemented wrongly (probably on wrong layers). Introducing additional dropout layers would probably be more helpful.

