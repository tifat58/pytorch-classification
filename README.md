# Pytorch Classification

- A general, feasible and extensible framework for 2D image classification.



## Features

- Easy to configure (model, hyperparameters)
- Training progress monitoring and visualization
- Weighted sampling / weighted loss / kappa loss / focal loss for imbalance dataset
- Kappa metric for evaluating model on imbalance dataset
- Different learning rate schedulers and warmup support
- Data augmentation
- Multiple GPUs support



## Installation

Recommended environment:
- python 3.8+
- pytorch 1.7.1+
- torchvision 0.8.2+
- tqdm
- munch
- packaging
- tensorboard

To install the dependencies, run:
```shell
$ git clone https://github.com/YijinHuang/pytorch-classification.git
$ cd pytorch-classification
$ pip install -r requirements.txt
```



## How to use

**1. Use one of the following two methods to build your dataset:**

- Folder-form dataset:

Organize your images as follows:

```
├── your_data_dir
    ├── train
        ├── class1
            ├── image1.jpg
            ├── image2.jpg
            ├── ...
        ├── class2
            ├── image3.jpg
            ├── image4.jpg
            ├── ...
        ├── class3
        ├── ...
    ├── val
    ├── test
```

Here, `val` and `test` directory have the same structure of  `train`.  Then replace the value of 'data_path' in BASIC_CONFIG in `configs/default.yaml` with path to your_data_dir and keep 'data_index' as null.

- Dict-form dataset:

Define a dict as follows:

```python
your_data_dict = {
    'train': [
        ('path/to/image1', 0), # use int. to represent the class of images (start from 0)
        ('path/to/image2', 0),
        ('path/to/image3', 1),
        ('path/to/image4', 2),
        ...
    ],
    'test': [
        ('path/to/image5', 0),
        ...
    ],
    'val': [
        ('path/to/image6', 0),
        ...
    ]
}
```

Then use pickle to save it:

```python
import pickle
pickle.dump(your_data_dict, open('path/to/pickle/file', 'wb'))
```

Finally, replace the value of 'data_index' in BASIC_CONFIG in `configs/default.yaml` with 'path/to/pickle/file' and set 'data_path' as null.

**2. Update your training configurations and hyperparameters in `configs/default.yaml`.**

**3. Run to train:**

```shell
$ CUDA_VISIBLE_DEVICES=x python main.py
```

Optional arguments:
```
-c yaml_file      Specify the config file (default: configs/default.yaml)
-o                Overwrite save_path and log_path without warning
-p                Print configs before training
```

**4. Monitor your training progress in website [127.0.0.1:6006](127.0.0.1:6006) by running:**

```shell
$ tensorborad --logdir=/path/to/your/log --port=6006
```

[Tips to use tensorboard on a remote server](https://blog.yyliu.net/remote-tensorboard/)