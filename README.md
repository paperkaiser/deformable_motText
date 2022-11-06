# deformable_mottext






## Installation
The codebases are built on top of [Deformable DETR](https://github.com/fundamentalvision/Deformable-DETR) and [MOTR](https://github.com/megvii-model/MOTR).

* Linux, CUDA=9.2, GCC=7.1.0, Python=3.7

  
* install requirements
    ```bash
    pip install -r requirements.txt
    ```

* Build MultiScaleDeformableAttention and Rotated ROIAlign
    ```bash
    sh models/ops/make.sh
	
    python models/Rotated_ROIAlign/setup.py build_ext --inplace
    ```

### Datasets 

1.  Download [ICDAR2015](https://rrc.cvc.uab.es/?ch=3&com=evaluation&task=4) and [COCOTextV2 dataset](https://bgshih.github.io/cocotext/) and organize them like [FairMOT](https://github.com/ifzhang/FairMOT) as following:

```
.
├── COCOText
│   ├── images
│   └── labels_with_ids
├── ICDAR15
│   ├── train
│       ├── frames
│           ├── Video_8_5_1
│           ├── Video_7_5_1
│                  ...
│       ├── labels
│           ├── Video_8_5_1
│           ├── Video_7_5_1
│                  ...
│   ├── test
│       ├── frames
│           

```

2. Generate labels file:


```bash 
cd tools/gen_labels
python3 gen_labels_COCOTextV2.py
python3 gen_labels_ICDAR15_video.py
```
### Training and Evaluation

#### Training

 Training on COCOTextV2 :
```bash 
sh configs/r50_pretrain_COCOText.sh
```

Training on ICDAR2015 :

```bash 
sh configs/r50_train_ICDAR15video.sh
```
You can change the numbers of GPU, lr_drop, two_stage and sampler_lengths to better performence(for example: change the sampler_lengths to 7 or 9)

Change the sample_interval to adapt to different frame rates

.......
#### Evaluation on ICDAR15


```bash 
sh configs/r50_eval_ICDAR2015.sh
```


