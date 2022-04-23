# Pytorch Implementation of GOLDNet
[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

This repository contains code for an image segmentation model based on Nested UNet (Inculdes UNet).

## Requirements
- PyTorch 1.x
- Albumentations 0.1.12
- Pandas 1.x.x

## Installation
`pip install -r requriements`

## Training on custom dataset
Make sure to put the files as the following structure (e.g. the number of classes is 2):
```
inputs
└── <dataset name>
    ├── images
    |   ├── 0a7e06.jpg
    │   ├── 0aab0a.jpg
    │   ├── 0b1761.jpg
    │   ├── ...
    |
    └── masks
        ├── 0
        |   ├── 0a7e06.png
        |   ├── 0aab0a.png
        |   ├── 0b1761.png
        |   ├── ...
        |
        └── 1
            ├── 0a7e06.png
            ├── 0aab0a.png
            ├── 0b1761.png
            ├── ...
```
The file format doesn't matter, it can be modified with the training command.

1. Train the model

`python train.py --dataset <dataset name> --arch NestedUNet --img_ext .jpg --mask_ext .png`

```
usage: train.py [-h] [--name NAME] [--epochs N] [-b N] [--arch ARCH]
                [--deep_supervision DEEP_SUPERVISION]
                [--input_channels INPUT_CHANNELS] [--num_classes NUM_CLASSES]
                [--input_w INPUT_W] [--input_h INPUT_H]
                [--loss {BCEDiceLoss,LovaszHingeLoss,BCEWithLogitsLoss}]
                [--dataset DATASET] [--img_ext IMG_EXT] [--mask_ext MASK_EXT]
                [--optimizer {Adam,SGD}] [--lr LR] [--momentum MOMENTUM]
                [--weight_decay WEIGHT_DECAY] [--nesterov NESTEROV]
                [--scheduler {CosineAnnealingLR,ReduceLROnPlateau,MultiStepLR,ConstantLR}]
                [--min_lr MIN_LR] [--factor FACTOR] [--patience PATIENCE]
                [--milestones MILESTONES] [--gamma GAMMA] [--early_stopping N]
                [--num_workers NUM_WORKERS]

optional arguments:
  -h, --help            show this help message and exit
  --name NAME           model name: (default: arch+timestamp)
  --epochs N            number of total epochs to run
  -b N, --batch_size N  mini-batch size (default: 16)
  --arch ARCH, -a ARCH  model architecture: GOLDNet (default: GOLDNet)
  --deep_supervision DEEP_SUPERVISION
  --input_channels INPUT_CHANNELS
                        input channels
  --num_classes NUM_CLASSES
                        number of classes
  --input_w INPUT_W     image width
  --input_h INPUT_H     image height
  --loss {BCEDiceLoss,LovaszHingeLoss,BCEWithLogitsLoss}
                        loss: BCEDiceLoss | LovaszHingeLoss |
                        BCEWithLogitsLoss (default: BCEDiceLoss)
  --dataset DATASET     dataset name
  --img_ext IMG_EXT     image file extension
  --mask_ext MASK_EXT   mask file extension
  --optimizer {Adam,SGD}
                        loss: Adam | SGD (default: Adam)
  --lr LR, --learning_rate LR
                        initial learning rate
  --momentum MOMENTUM   momentum
  --weight_decay WEIGHT_DECAY
                        weight decay
  --nesterov NESTEROV   nesterov
  --scheduler {CosineAnnealingLR,ReduceLROnPlateau,MultiStepLR,ConstantLR}
  --min_lr MIN_LR       minimum learning rate
  --factor FACTOR
  --patience PATIENCE
  --milestones MILESTONES
  --gamma GAMMA
  --early_stopping N    early stopping (default: -1)
  --num_workers NUM_WORKERS
```

2. Evaluate

`python val.py --name <model name>`
