# About

Use DCGAN to create trippy videos:

<a href="https://www.vjloops.com/stock-video/fresh-and-simple-7-loop-3-140717.html">![](https://storage.googleapis.com/vjloops/140717_thumb0.jpg)</a>
<a href="https://www.vjloops.com/stock-video/fresh-and-simple-8-loop-3-140747.html">![](https://storage.googleapis.com/vjloops/140747_thumb0.jpg)</a>

[More examples on my portfolio](https://www.vjloops.com/users/20585.html)

The model is based on [carpedm20/DCGAN-tensorflow](https://github.com/carpedm20/DCGAN-tensorflow).

# Usage

    python3 multitrain.py --config my_config.csv 
    
Or with `nohup`:
   
    nohup python3 multitrain.py --config my_config.csv > log.out 2>&1&

Other command parameters:

* ```--gpu_idx 2``` to pick a GPU device if you have multiple of them
* ```--disable_cache``` disable caching of np data (you should add that if you use a lot of images) 

The CSV file contains a list of jobs with different model and video parameters.
A minimal config CSV file must contain the following columns:

|name          |dataset       |grid_width|grid_height|video_length|
|---           |---           |---       |---        |---         |
|job01         |images_folder |3         |3          |5           |
|job02         |images_folder |3         |3          |5           |

* `name`: name of the job, to create the checkpoint, the name of the video, etc.
* `dataset`: image folders where the input images are
    * must be a subfolder of `/data/`
    * images are fetched recursively in folders and subfolders
    * you can add multiple folders with a comma: `images_folder1,images_folder2,images_folder3`
    * all images must be the same size 
* `video_length`: length of the output video in minutes

More columns can be added with the parameters described below:

## Model Parameters

#### Layers
* `nbr_of_layers_g` and `nbr_of_layers_d`: Number of layers in the Generator and in the Discriminator.
* Default value: `5`
   
#### Activation Functions
* `activation_g` and `activation_d`: Activation function between layers of the Generator and the Discriminator. 
* Default values are `relu` and `lrelu`.
* Possible values: `relu`, `relu6`, `lrelu`, `elu`, `crelu`, `selu`, `tanh`, `sigmoid`, `softplus`, `softsign`, `softmax`, `swish`.
    
#### Adam Optimizer

* `learning_rate_g`, `beta1_g`, `learning_rate_d`, `beta1_d`:

|Parameter          |TensorFlow default|DCGAN default|
|---                |---               |---          |
|**Learning rate**  |0.001             |0.0002       |
|**Beta1**          |0.9               |0.5          |

## Video Parameters

# Dependencies

## Python libs
```
(tensorflow4) benoit@farm:~$ pip3 list
Package              Version 
-------------------- --------
absl-py              0.7.1   
astor                0.7.1   
cffi                 1.12.2  
cloudpickle          0.8.1   
gast                 0.2.2   
grpcio               1.19.0  
h5py                 2.9.0   
horovod              0.16.1  
Keras-Applications   1.0.7   
Keras-Preprocessing  1.0.9   
Markdown             3.1     
mock                 2.0.0   
numpy                1.16.2  
opencv-python        4.0.0.21
pandas               0.24.2  
pbr                  5.1.3   
Pillow               5.4.1   
pip                  19.0.3  
protobuf             3.7.1   
psutil               5.6.1   
pycparser            2.19    
python-dateutil      2.8.0   
pytz                 2018.9  
scipy                1.2.1   
setuptools           39.1.0  
six                  1.12.0  
tensorboard          1.13.1  
tensorflow-estimator 1.13.0  
tensorflow-gpu       1.13.1  
termcolor            1.1.0   
Werkzeug             0.15.1  
wheel                0.33.1 
```

## Set-up

* Linux Mint 19.1 (Ubuntu 18.04)
* TensorFlow 1.13.0
* Cuda 10
* cudnn 7.5.0
* Nvidia driver 417 

# Credit

See [the original project](https://github.com/carpedm20/DCGAN-tensorflow) 
and Taehoon Kim / [@carpedm20](http://carpedm20.github.io/) for more info