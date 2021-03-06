# CATS - Deep Convolutional Generative Adversarial Network

This repository serves as an example of how to generate images of cat faces using a [Deep Convolutional Generative Adversarial Network](https://arxiv.org/pdf/1511.06434.pdf) (DCGAN) developed by [@Rapsssito](https://github.com/rapsssito) and [@pablotix20](https://github.com/pablotix20). It is heavily inspired by [TensorFlow's tutorial](https://www.tensorflow.org/tutorials/generative/dcgan) about this topic. This repository does not provide a training dataset, but several are available online:
 * [`fferlito/Cat-faces-dataset`](https://github.com/fferlito/Cat-faces-dataset)
 * [`Cats faces 64x64`](https://www.kaggle.com/spandan2/cats-faces-64x64-for-generative-models)

## Our model
Our particular model, provided in [cats_gan.ipynb](./cats_gan.ipynb), uses more than 30k 64x64 resized RGB images of cat faces as the training dataset. Below the structures for the generator and discriminator are provided:

### Generator structure
```
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
dense (Dense)                (None, 50)                2500      
_________________________________________________________________
batch_normalization (BatchNo (None, 50)                200       
_________________________________________________________________
leaky_re_lu (LeakyReLU)      (None, 50)                0         
_________________________________________________________________
reshape (Reshape)            (None, 1, 1, 50)          0         
_________________________________________________________________
conv2d_transpose (Conv2DTran (None, 2, 2, 512)         921600    
_________________________________________________________________
batch_normalization_1 (Batch (None, 2, 2, 512)         2048      
_________________________________________________________________
leaky_re_lu_1 (LeakyReLU)    (None, 2, 2, 512)         0         
_________________________________________________________________
conv2d_transpose_1 (Conv2DTr (None, 4, 4, 256)         4718592   
_________________________________________________________________
batch_normalization_2 (Batch (None, 4, 4, 256)         1024      
_________________________________________________________________
leaky_re_lu_2 (LeakyReLU)    (None, 4, 4, 256)         0         
_________________________________________________________________
conv2d_transpose_2 (Conv2DTr (None, 8, 8, 128)         1179648

=================================================================
Total params: 7,215,372
Trainable params: 7,213,256
Non-trainable params: 2,116
```

### Discriminator structure
```
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
conv2d_18 (Conv2D)           (None, 32, 32, 16)        1744      
_________________________________________________________________
leaky_re_lu_25 (LeakyReLU)   (None, 32, 32, 16)        0         
_________________________________________________________________
dropout_18 (Dropout)         (None, 32, 32, 16)        0         
_________________________________________________________________
conv2d_19 (Conv2D)           (None, 16, 16, 32)        18464     
_________________________________________________________________
leaky_re_lu_26 (LeakyReLU)   (None, 16, 16, 32)        0         
_________________________________________________________________
dropout_19 (Dropout)         (None, 16, 16, 32)        0         
_________________________________________________________________
conv2d_20 (Conv2D)           (None, 8, 8, 64)          73792     
_________________________________________________________________
leaky_re_lu_27 (LeakyReLU)   (None, 8, 8, 64)          0         
_________________________________________________________________
dropout_20 (Dropout)         (None, 8, 8, 64)          0         
_________________________________________________________________
conv2d_21 (Conv2D)           (None, 4, 4, 128)         295040    
_________________________________________________________________
leaky_re_lu_28 (LeakyReLU)   (None, 4, 4, 128)         0

Total params: 6,288,561
Trainable params: 6,288,561
Non-trainable params: 0
```

### Experiment
An experiment with 3484 epochs provided the following results:

![docs/cats_gan.gif](docs/cats_gan.gif)

#### Generator and discriminator losses
![docs/loss_chart.jpg](docs/loss_chart.jpg)

#### 16 sample images (epoch 0301)
![docs/image_at_epoch_0301.png](docs/image_at_epoch_0301.png)

#### 16 sample images (epoch 3476)
![docs/image_at_epoch_3476.png](docs/image_at_epoch_3476.png)
