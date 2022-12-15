# Assignment 6 training logs

## DDP Strategy

```bash
loss: 0.259 v_num: 0 val/loss: 1.704 val/acc: 0.683 val/acc_best: 0.689 train/loss: 0.165 train/acc: 0.948
```
No. of epochs: 25

Highest batch size: 8192

S3 URI for best checkpoint: s3://emlov2-s3-yaseen/assignment6/ddp_bs8192.ckpt

Training time: 1944.99 s

Train acc: 0.948

Best val acc: 0.689

Test acc: 0.694

Experiment folders:
 - Train : https://tensorboard.dev/experiment/xuxLlEYnSr6MZXSDKUKaEQ/
 - Test : https://tensorboard.dev/experiment/vGqgltrJTBGpbgg5UgF2xw/

GPU Usage:
```
Wed Dec 14 18:45:41 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 510.73.08    Driver Version: 510.73.08    CUDA Version: 11.6     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla T4            On   | 00000000:00:1E.0 Off |                    0 |
| N/A   47C    P0    38W /  70W |   3539MiB / 15360MiB |     98%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      4556      C   ...a/envs/pytorch/bin/python     3537MiB |
+-----------------------------------------------------------------------------+
```

## FSDP Strategy

```bash
loss: 2.45 v_num: 0 val/loss: 2.236 val/acc: 0.203 val/acc_best: 0.252 train/loss: 2.422 train/acc: 0.252
```
No. of epochs: 5

Highest batch size: 16384

S3 URI for best checkpoint: s3://emlov2-s3-yaseen/assignment6/fsdp_bs16384.ckpt

Training time: 128.45 s

Train acc: 0.252

Best val acc: 0.252

Test acc: 0.259

Experiment folders:
 - Train : https://tensorboard.dev/experiment/D6Qw3IBdQ6ahwyZf9xVRSA/
 - Test : https://tensorboard.dev/experiment/3mDiesZ8SgC1pt4YNI62VQ/

GPU Usage:
```
Thu Dec 15 02:31:52 2022
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 510.73.08    Driver Version: 510.73.08    CUDA Version: 11.6     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla T4            On   | 00000000:00:1E.0 Off |                    0 |
| N/A   46C    P0    37W /  70W |   3399MiB / 15360MiB |    100%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A     19935      C   python                           3397MiB |
+-----------------------------------------------------------------------------+
```
