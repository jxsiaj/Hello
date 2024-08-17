**paper at the PDET: Progressive Diversity Expansion Transformer for Cross-Modality Visible-Infrared Person Re-identification**

**Person Re-identifification**

### 1. Results
We adopt the Transformer-based ViT-Base/16 as backbone respectively.

|Datasets    | Backbone | Rank@1  | mAP |  mINP |  Model|
| --------   | -----    | -----  |  -----  | ----- |:----:|
| #SYSU-MM01 | ViT | ~ 68.36% | ~ 66.42% | ~53.80% |[GoogleDrive](https://drive.google.com/file/d/1VfHGeZbE2ut-5hd8fU0Qz8gs_i563Knl/view?usp=drive_link)|

### 2. Datasets

- (1) RegDB [1]: The RegDB dataset can be downloaded from this [website](http://dm.dongguk.edu/link.html).

- (2) SYSU-MM01 [2]: The SYSU-MM01 dataset can be downloaded from this [website](http://isee.sysu.edu.cn/project/RGBIRReID.htm).

### 3. Requirements

#### **Prepare Pre-trained Model**

- You may need to download the ImageNet pretrained transformer model [ViT-Base](https://github.com/rwightman/pytorch-image-models/releases/download/v0.1-vitjx/jx_vit_base_p16_224-80ecf9dd.pth).

#### Prepare Training Data
- You need to define the data path and pre-trained model path in `config.py`.
- You need to run `python process_sysu.py` to pepare the dataset, the training data will be stored in ".npy" format.


### 4. Training

**Train PEDT by**

```
python train.py --config_file config/SYSU.yml 

or 

python train.py --config_file config/RegDB.yml

```
  - `--config_file`:  the config file path.

### 5. Testing

**Test a model on SYSU-MM01 dataset by**

```
python test.py --dataset 'sysu' --mode 'all' --resume 'model_path' --gall_mode 'single' --gpu 0
```
  - `--dataset`: which dataset "sysu" or "regdb".
  - `--mode`: "all" or "indoor"  (only for sysu dataset).
  - `--gall_mode`: "single" or "multi" (only for sysu dataset).
  - `--resume`: the saved model path.
  - `--gpu`: which gpu to use.

**Test a model on RegDB dataset by**

```
python test.py --dataset 'regdb' --resume 'model_path' --trial 1 --tvsearch True --gpu 0
```

  - `--trial`: testing trial should match the trained model  (only for regdb dataset).

  - `--tvsearch`:  whether thermal to visible search  True or False (only for regdb dataset).



### 6. Citation

Most of the code of our backbone are borrowed from [TransReID](https://github.com/damo-cv/TransReID) [3]

Thanks a lot for the author's contribution.

Please cite the following paper in your publications if it is helpful:

```

@inproceedings{he2021transreid,
  title={Transreid: Transformer-based object re-identification},
  author={He, Shuting and Luo, Hao and Wang, Pichao and Wang, Fan and Li, Hao and Jiang, Wei},
  booktitle={Proceedings of the IEEE/CVF international conference on computer vision},
  pages={15013--15022},
  year={2021}
}

```

###  7. References.

[1] D. T. Nguyen, H. G. Hong, K. W. Kim, and K. R. Park. Person recognition system based on a combination of body images from visible light and thermal cameras. Sensors, 17(3):605, 2017.

[2] A. Wu, W.-s. Zheng, H.-X. Yu, S. Gong, and J. Lai. Rgb-infrared crossmodality person re-identification. In IEEE International Conference on Computer Vision (ICCV), pages 5380–5389, 2017.

[3] He S, Luo H, Wang P, et al. Transreid: Transformer-based object re-identification[C]//Proceedings of the IEEE/CVF international conference on computer vision. 2021: 15013-15022.
