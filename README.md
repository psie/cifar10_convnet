This is a convolutional neural network in python.
The code is an ipython notebook (if you are on github you can probably even view it online). Libraries used are fuel, theano and lasagne. 
This is an experiment for the Neural Network course at University of Technology:

https://sites.google.com/a/cs.uni.wroc.pl/jch/teaching/neuralnetworks15

Test data is a set of 60 000 32x32 color images called CIFAR10.
Training data (50 000 samples) is split into two sets:
* training set (images 1 - 40 000)
* validation set (images 40 001 - 50 000)
Test data consists of remaining 10 000 samples.

Currently the network achieves around 80% accuracy. 

Files:
* convnet.ipynb - source code
* params.bin - parameters of a trained network
* restuls - results on the test set. Format: classifier_output real_label 

Preprocessing done on the data - scaling of data from channels color channels with results saved into 32-bit float numbers.

Layers used: 
* Convolutional layers with linear rectifier
* 2D MaxPool layers
* Dropout layer
* Softmax layer

Network architecture:

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

Current problems:
* Architecture of this network renders training on CPUs rather infeasible (long computations).
* Overfitting - network tends to fit to the training data too closely, sacraficing generality and resulting worse on the validation and test sets. I tried implementing some sort of regularization to overcome the problem but apparently it is implemented wrongly (probably on wrong layers). Introducing additional dropout layers would probably be more helpful.

