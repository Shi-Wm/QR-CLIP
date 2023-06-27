# <p align=center>`QR-CLIP`</p><!-- omit in toc -->

## Table of Contents

  * [Introduction](#1-introduction)
  * [Requirements](#2-requirements)
  * [Download Datasets and Pre-trained model](#3-download-Datasets-and-Pre-trained-model)
  * [The file structure](#4-the-file-structure)
  * [Running](#5-running)

## 1. Introduction

##  2. Requirements 

**Creat Anaconda virtual environment.**
```
conda create --name QR-CLIP python=3.8.5  
conda activate QR-CLIP
```
**Install [PyTorch 1.10.1](https://pytorch.org/get-started/locally) (or later) and torchvision, as well as small additional dependencies. The following will do the trick:**

```
conda install pytorch==1.10.1 torchvision==0.11.2 torchaudio==0.10.1 -c pytorch
pip install pandas
pip install transformers
```
**Prepare for finetuned clip.**

* Since the ```original CLIP``` did not open source the finetune process, we used the code in [OpenCLIP](https://github.com/mlfoundations/open_clip) to finetune the CLIP. [OpenCLIP](https://github.com/mlfoundations/open_clip) is a faithful reproduction of ```original CLIP```. It can be used by the following command:
```
pip install open_clip_torch
```

##  3. Download Datasets and Pre-trained model
**Datasets:**
* `image.zip`

Download from [Goole Drive](https://drive.google.com/file/d/1aHu9nbdmnQ8SDr-0P7VySLsKxl54SUQp/view?usp=sharing). 

Also you could quikcly download by running:

```
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1aHu9nbdmnQ8SDr-0P7VySLsKxl54SUQp' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1aHu9nbdmnQ8SDr-0P7VySLsKxl54SUQp" -O image.zip && rm -rf /tmp/cookies.txt
```

**Pre-trained model:**
*  `VIT-B-32.pt`

Download from [Goole Drive](https://drive.google.com/file/d/1-2Q5f9igvFC6S6mYapoYRWvDQsbPXIqr/view?usp=sharing).

Also you could quikcly download by running:
```
wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate 'https://docs.google.com/uc?export=download&id=1-2Q5f9igvFC6S6mYapoYRWvDQsbPXIqr' -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')&id=1-2Q5f9igvFC6S6mYapoYRWvDQsbPXIqr" -O vit-b-32-4cls.pt && rm -rf /tmp/cookies.txt
```

## 4. The file structure

```
---- QR-CLIP
-------- checkpoints
------------ VIT-B-32.pt # pre-training model of clip
-------- data
------------image
------------ train.txt  # Training label file
------------ location_test.txt  # Location label test file
------------ time_test.txt  # Time label test file
-------- main
------------ owk 
------------------- top20_1019.csv # 120,000 open world knowledge
------------ experiment_reslts # Save training results
------------ ft_clip_4cls-max.py  # Our method
------------ test.py # test code
------------ search_owk.py # Obtain open world knowledge with 4 cls
-------- utils
```

##  5. Running 

```
conda activate QR-CLIP
cd QR-CLIP/main/
```
**Training model**
```
mkdir experiment_reslts
python ft_clip_4cls-max.py
```

**Obtaining open world knowledge**
```
python search_owk.py
```

**Testing model**
```
python test.py
```
