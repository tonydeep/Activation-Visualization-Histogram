# SELUs (scaled exponential linear units) - Visualized and Histogramed Comparison among ReLU and Leaky ReLU

## Descriptions
This project includes a [Tensorflow](https://www.tensorflow.org/) implementation of SELUs (scaled exponential linear units) proposed in this paper [Self-Normalizing Neural Networks](https://arxiv.org/abs/1706.02515). Also, aiming to present clear at a glance comparisons among SELU, ReLU, Leaky ReLU, etc, this implementation focuses on visualizing and histograming activations on [Tensorboard](https://www.tensorflow.org/get_started/summaries_and_tensorboard). As a result, the draw nvisualization and histogram are nicely incorporate with Tensorboard by introducing plotting summaries. Examples of visualizaion and histogram are as follow.

<img src="figure/AVH.png" height="300"/>, 

Ideally, desire activations of every layer are close to *zero mean* and *unit variance* to make tensors propagated through several layers converge towards zero mean and unit variance. The learning can, therefore, be stabilized by preventing gradients from being vanishing and exploding. In this work, the authors propose scaled exponential linear units (SELUs) which aim to automatically shift and rescale neuron activations towards zero mean and unit variance without explicit normalization like what batch normalization technique does. 

Intending to empirically verify the effectiveness of the proposed activations, a convolutional neural network consisting of three convolutional layers followed by three fully conneted layers was implemented to be trained on image classification tasks on datasets such as MNIST, SVHN, and CIFAR10. To overcome the limited content allowed to be shown on Tensorboard, a ploting library [Tensorflow Plot](https://github.com/wookayin/tensorflow-plot) aiming to bridge the gap between Python plotting library and Tensorboard is introduced. Again, here are some examples.

* Histogram of activations on Tensorboard

<img src="figure/H.png" height="150"/>, 

* Visualization of activations on Tensorboard

<img src="figure/V.png" height="150"/>, 

The implemented model is trained and tested on three publicly available datasets: [MNIST](http://yann.lecun.com/exdb/mnist/), [SVHN](http://ufldl.stanford.edu/housenumbers/), and [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html).

\*This code is still being developed and subject to change.

## Prerequisites

- Python 2.7 or Python 3.3+
- [Tensorflow 1.0.0](https://github.com/tensorflow/tensorflow/tree/r1.0)
- [Tensorflow Plot](https://github.com/wookayin/tensorflow-plot)
- [SciPy](http://www.scipy.org/install.html)
- [NumPy](http://www.numpy.org/)

## Usage

Download datasets with:
```bash
$ python download.py --dataset MNIST SVHN CIFAR10
```
Simpy run comparisons among the default activations including SELU, ReLU, and Leaky ReLU
```bash
python script.py
```
Train models with different activation functions with downloaded datasets:
```bash
$ python trainer.py --dataset MNIST --activation relu
$ python trainer.py --dataset SVHN --activation lrelu
$ python trainer.py --dataset CIFAR10 --activation selu
```
Train and test your own datasets:

* Create a directory
```bash
$ mkdir datasets/YOUR_DATASET
```

* Store your data as an h5py file datasets/YOUR_DATASET/data.hy and each data point contains
    * 'image': has shape [h, w, c], where c is the number of channels (grayscale images: 1, color images: 3)
    * 'label': represented as an one-hot vector
* Maintain a list datasets/YOUR_DATASET/id.txt listing ids of all data points
* Modify trainer.py including args, data_info, etc.
* Finally, train and test models:
```bash
$ python trainer.py --dataset YOUR_DATASET
$ python evaler.py --dataset YOUR_DATASET
```
## Results

### MNIST
<!--
* Generated samples (100th epochs)

<img src="figure/result/mnist/samples.png" height="250"/>

* First 40 epochs
<img src="figure/result/mnist/training.gif" height="250"/>
-->
### SVHN

<!--
* Generated samples (100th epochs)

<img src="figure/result/svhn/samples.png" height="250"/>

* First 160 epochs

<img src="figure/result/svhn/training.gif" height="250"/>
-->

### CIFAR-10

<!--
* Generated samples (1000th epochs)

<img src="figure/result/cifar10/samples.png" height="250"/>

* First 200 epochs

<img src="figure/result/cifar10/training.gif" height="250"/>
-->

## Training details

### MNIST

### SVHN

### CIFAR-10

## Training tricks

* To avoid the fast convergence of the discriminator network
    * The generator network is updated more frequently.
    * Higher learning rate is applied to the training of the generator.
* One-sided label smoothing is applied to the positive labels.
* Gradient clipping trick is applied to stablize training
* Reconstruction loss with an annealed weight is applied as an auxiliary loss to help the generator get rid of the initial local minimum.
* Utilize [Adam](https://arxiv.org/abs/1412.6980) optimizer with higher momentum.
* Please refer to the codes for more details.

## Related works
* [Self-Normalizing Neural Networks](https://arxiv.org/pdf/1706.02515.pdf) by Klambauer et. al
* [Rectified Linear Units Improve Restricted Boltzmann Machines](http://www.cs.toronto.edu/~fritz/absps/reluICML.pdf) by Nair et. al.
* [Empirical Evaluation of Rectified Activations in Convolutional Network](https://arxiv.org/abs/1505.00853) by Xu et. al.

## Author

Shao-Hua Sun / [@shaohua0116](https://shaohua0116.github.io/)

The code *monitor.py* was written by Jongwook Choi / [@wookayin](https://github.com/wookayin/)
