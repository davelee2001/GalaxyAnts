# Galaxy Ants
<a href="https://pypi.org/project/vmas"><img src="https://img.shields.io/pypi/v/vmas" alt="pypi version"></a>
[![Downloads](https://static.pepy.tech/personalized-badge/vmas?period=total&units=international_system&left_color=grey&right_color=blue&left_text=Downloads)](https://pepy.tech/project/vmas)
![tests](https://github.com/proroklab/VectorizedMultiAgentSimulator/actions/workflows/python-app.yml/badge.svg)
[![Python](https://img.shields.io/badge/python-3.8%20%7C%203.9%20%7C%203.10-blue.svg)](https://www.python.org/downloads/)
[![GitHub license](https://img.shields.io/badge/license-GPLv3.0-blue.svg)](https://github.com/proroklab/VectorizedMultiAgentSimulator/blob/main/LICENSE)

<p align="center">
<img src="https://github.com/matteobettini/vmas-media/blob/main/media/VMAS_scenarios.gif?raw=true" alt="drawing"/>  
</p>

## Welcome to Galaxy Ants!

Galaxy Ants is an aerospace intelligent control algorithm service platform. The algorithm provider uploads cutting-edge intelligent control algorithms to this platform. The algorithm user can download the algorithm to the local machine for secondary development, or use tools such as Docker, Vercel to achieve one-click deployment.


## Table of contents

- [Galaxy Ants](#galaxy-ants)
  * [Welcome to Galaxy Ants!](#welcome-to-galaxy-ants!)
  * [Table of contents](#table-of-contents)
  * [How to use](#how-to-use)
    + [Notebooks](#notebooks)
    + [Install](#install)
  * [Background](#background)
    + [Notebooks](#business-motivation)
    + [Install](#innovation)
  * [Algorithm Design](#algorithm-design)
  * [Results](#results)
    + [Intuitive](#intuitive)
    + [Install](#efficiency)
  * [Main Contributors](#how-to-use)

## How to use
### Notebooks
-  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/10R6KIRG5grpBFBDUI5njTcKvZ2rqsaWd?usp=share_link) &ensp; **Running oline**.
 Here is a simple notebook that you can run to create, step and render a senario using multi-agent reinforcement learning algorithm.

### Install

If you want to install the current master version (more up to date than latest release), you can do:
```
git clone https://github.com/davelee2001/GalaxyAnts.git
cd VectorizedMultiAgentSimulator
pip install -e .
```
By default, GalaxyAnts has only the core requirements. Here are some optional packages you may want to install:
```
# Training
pip install "ray[rllib]"==2.2 # We support versions "ray[rllib]<=2.2,>=1.13"
pip install torchrl

# Logging
pip installl wandb 

# Save renders
pip install opencv-python moviepy

# Tests
pip install pytest pyyaml pytest-instafail tqdm
```


## Background
### Business Motivation
### Innovation

## Algorithm Design

## Results
### Intuitive
### Efficiency


