<div align="center">

# EMLO 2.0 Assignment 6

<a href="https://pytorch.org/get-started/locally/"><img alt="PyTorch" src="https://img.shields.io/badge/PyTorch-ee4c2c?logo=pytorch&logoColor=white"></a>
<a href="https://pytorchlightning.ai/"><img alt="Lightning" src="https://img.shields.io/badge/-Lightning-792ee5?logo=pytorchlightning&logoColor=white"></a>
<a href="https://hydra.cc/"><img alt="Config: Hydra" src="https://img.shields.io/badge/Config-Hydra-89b8cd"></a>
<a href="https://github.com/ashleve/lightning-hydra-template"><img alt="Template" src="https://img.shields.io/badge/-Lightning--Hydra--Template-017F2F?style=flat&logo=github&labelColor=gray"></a><br>
[![Paper](http://img.shields.io/badge/paper-arxiv.1001.2234-B31B1B.svg)](https://www.nature.com/articles/nature14539)
[![Conference](http://img.shields.io/badge/AnyConference-year-4b44ce.svg)](https://papers.nips.cc/paper/2020)

</div>

## Description

This project trains timm models on multiple gpus existing over multiple nodes. This assignment involves using two strategies : DDP and FSDP for the task.

## How to run

Install dependencies

```bash
# clone project
git clone https://github.com/MohammedYaseen97/emlov2-assignment6
cd emlov2-assignment6

# [OPTIONAL] create conda environment
conda create -n myenv python=3.8
conda activate myenv

# install pytorch according to instructions
# https://pytorch.org/get-started/

# install requirements
pip install -r requirements.txt
```

Train model with default configuration

```bash
# train on CPU
python src/train.py trainer=cpu

# train on GPU
python src/train.py trainer=gpu
```

Train model with chosen experiment configuration from [configs/experiment/](configs/experiment/)

```bash
python src/train.py experiment=experiment_name.yaml
```

You can override any parameter from command line like this

```bash
python src/train.py trainer.max_epochs=20 datamodule.batch_size=64
```

## Multi GPU training

DDP strategy can be used as follows:

```bash
MASTER_PORT=29500 MASTER_ADDR=172.31.47.183 WORLD_SIZE=4 NODE_RANK=0 python src/train.py trainer=ddp trainer.devices=1 trainer.num_nodes=4 experiment=cifar trainer.default_root_dir=$(date + %Y-%m-%d_%H-%M-%S) callbacks.model_checkpoint.dirpath=logs/train/runs datamodule.num_workers=8
```
The extra nodes can be added as follows:

```bash
MASTER_PORT=29500 MASTER_ADDR=172.31.47.183 WORLD_SIZE=4 NODE_RANK=1 python src/train.py trainer=ddp trainer.devices=1 trainer.num_nodes=4 experiment=cifar trainer.default_root_dir=$(date + %Y-%m-%d_%H-%M-%S) callbacks.model_checkpoint.dirpath=logs/train/runs datamodule.num_workers=8
```

FSDP strategy can be used as follows:

```bash
MASTER_PORT=29500 MASTER_ADDR=172.31.47.183 WORLD_SIZE=2 NODE_RANK=0 python src/train.py trainer=fsdp trainer.devices=1 trainer.num_nodes=2 experiment=cifar trainer.default_root_dir=$(date + %Y-%m-%d_%H-%M-%S) callbacks.model_checkpoint.dirpath=logs/train/runs datamodule.num_workers=8 datamodule.batch_size=1024 trainer.max_epochs=5
```
The extra nodes can be added as follows:

```bash
MASTER_PORT=29500 MASTER_ADDR=172.31.47.183 WORLD_SIZE=2 NODE_RANK=1 python src/train.py trainer=fsdp trainer.devices=1 trainer.num_nodes=2 experiment=cifar trainer.default_root_dir=$(date + %Y-%m-%d_%H-%M-%S) callbacks.model_checkpoint.dirpath=logs/train/runs datamodule.num_workers=8 datamodule.batch_size=1024 trainer.max_epochs=5
```

Note that you cannot perform testing over multiple devices. That needs to be done separately on the single node (because the model checkpoints are saved here), like below:


```bash
python src/eval.py trainer=gpu model.net.model_name=vit_base_patch32_224 model.net.image_size=32 trainer.default_root_dir=$(date + %Y-%m-%d_%H-%M-%S) trainer.max_epochs=2 datamodule.num_workers=8 ckpt_path=logs/train/runs/epoch_001.ckpt
```
