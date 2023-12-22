## Installation
First please make sure modified OpenCLIP has been installed as follows
```
cd CLIM
pip install -e . -v
```
Then please refer to this [README](ovdet/INSTALLATION.md) to install the detector.

## Data Preparation
Please refer to this [README](ovdet/DATA.md).


## Usage
### Obtain Checkpoints
We provide checkpoints of models that are trained by CLIM in 
[Google Drive](https://drive.google.com/drive/folders/1v91n5SSXSOtgo2SlEESj_Gquwh9KMj3J?usp=sharing). Put them under 
`CLIM/ovdet/checkpoints`.

### Training
Take ViT-B/16 on OV-COCO as example, run the following to train the detector

```
cd CLIM/ovdet
bash tools/dist_train.sh \
     configs/clip_based/openai_vitb16/faster_rcnn_fpn_openai_vitb16_clim_bs64_ov_coco_3e.py 8 \
     --work-dir your/output/directory/ovdet_openai_vitb16_ov_coco_clim
```

### Testing
We also provide the following checkpoints of the trained detectors in 
[Google Drive](https://drive.google.com/drive/folders/1v91n5SSXSOtgo2SlEESj_Gquwh9KMj3J?usp=sharing). Download and 
put them under `CLIM/ovdet/checkpoints`. 

NOte: the released code for the ViT-based detector achieves better results than we have initially reported 
in the paper.

|  OV-COCO  | Backbone  | Novel AP50 |                                    Config                                     | Download  |
|:---------:|:--------:|:----------:|:-----------------------------------------------------------------------------:|:---------:|
|   Paper   | ViT-B/16 |    25.7    |                                       -                                       |     -     |
| This Repo | ViT-B/16 |    29.7    | [config](openai_vitb16/faster_rcnn_fpn_openai_vitb16_clim_bs64_ov_coco_3e.py) | [model](https://drive.google.com/file/d/1lOKpb2EiC2rcgsX9GeXUhVN1QnyUTZSM/view?usp=sharing) |



|  OV-LVIS  | Backbone | Mask APr |                                      Config                                       | Download  |
|:---------:|:--------:|:--------:|:---------------------------------------------------------------------------------:|:---------:|
|   Paper   | ViT-B/16 |   20.8   |                                         -                                         |     -     |
| This Repo | ViT-B/16 |   24.8   |  [config](openai_vitb16/mask_rcnn_nasfpn_openai_vitb16_clim_bs64_ov_lvis_4x.py)   | [model]() |
|   Paper   | RN50x64  |   32.3   |                                         -                                         |     -     |
| This Repo | RN50x64  |          | [config](openai_rn50x64/mask_rcnn_fpn_openai_rn50x64_clim_bs256_ov_lvis_2.88k.py) | [model]() |





Take ViT-B/16 on OV-COCO as example,  run the following to test the detector


```
cd CLIM/ovdet
bash tools/dist_train.sh tools/dist_test.sh \
     configs/clip_based/openai_vitb16/faster_rcnn_fpn_openai_vitb16_clim_bs64_ov_coco_3e.py \
     checkpoints/ovdet_openai_vitb16_ov_coco_clim.pth \
     8 --work-dir your/output/directory/ovdet_openai_vitb16_ov_coco_clim
```

