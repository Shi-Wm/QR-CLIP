# <p align=center>`QR-CLIP`</p><!-- omit in toc -->

## Table of Contents

  * [Introduction](#1-introduction)
  * [Requirements](#2-requirements)
  * [Download Datasets and Pre-trained model](#3-download-Datasets-and-Pre-trained-model)
  * [The file structure](#4-the-file-structure)
  * [Running](#5-running)

## Code Availability Statement
This code is associated with a paper currently under review. To comply with the review process, the code will be made publicly available once the paper is accepted. 

We appreciate your understanding and patience. Once the code is released, we will warmly welcome any feedback and suggestions. Please stay tuned for our updates!

## 1. Introduction
Daily images can convey abstract meanings that require us to memorize and infer profound information. To encourage human-like reasoning, in this work, we teach machines to predict where and when the image was captured.
Inspired by Hutchins's theory of Distributed Cognition, we design a new model called QR-CLIP, which is composed of two components. 1) The Quantity Module expands cognitive resources by accumulating as much open-world knowledge as possible from the environment, thereby enhancing cognitive ability. 2) The Relevance Module integrates relevant information from various cognitive tools to create a comprehensive cognitive outcome.
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
------------------- open world knowledge.csv # 120,000 open world knowledge
------------ experiment_reslts # Save training results
------------ 1-fine-tune.py  # Our method
------------ 2-search_owk.py # search open world knowledge with 6 cls
------------ 3-train_score.py
------------ test.py # test code
-------- utils
```

##  5. Running 

```
conda activate QR-CLIP
cd QR-CLIP/main/
```
**Location/Time Fine-tune**
```
mkdir experiment_reslts
python 1-fine-tune.py
```

**Searching open world knowledge**
```
python 2-search_owk.py
```

**Training Scoring Mechanism**
```
python 3-train_score.py
```

**Testing model**
```
python test.py
```
