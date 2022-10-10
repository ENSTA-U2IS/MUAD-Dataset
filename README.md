# MUAD: Multiple Uncertainties for Autonomous Driving Dataset

This repository contains some development kits (in PyTorch) that we used for our BMVC 2022 paper: 

MUAD: Multiple Uncertainties for Autonomous Driving, a benchmark for multiple uncertainty types and tasks.

[[Paper]](https://arxiv.org/abs/2203.01437) [[Website]](https://muad-dataset.github.io/) [[Challenge]](https://codalab.lisn.upsaclay.fr/competitions/8007)

For downloading the dataset, please go for the website shown above.

## Semantic segmentation

### Evaluation metrics
See folder `./evaluation_seg/`. This scoring program is also used in our [MUAD Challenge](https://codalab.lisn.upsaclay.fr/competitions/8007). Check `./evaluation_seg/evaluation.py` for details.

We provide the implementations on `mECE`, `mAUROC`, `mAUPR`, `mFPR`, `mIoU`, `mAccuracy`, etc., see `./evaluation_seg/stream_metrics.py` for details.

You have to make some modifications in the codes according to your own needs. For instance, we by default set our output confidence map as type `.pth`, and set only `mIOU` for semantic segmentation performance, etc.

### More information
The indexes of the classes of semantic segmentation are the following (in leftLabel):

| **class names**                       | **ID** |
|----------------------------------------|---------|
| road                                   | 0       |
| sidewalk                               | 1       |
| building                               | 2       |
| wall                                   | 3       |
| fence                                  | 4       |
| pole                                   | 5       |
| traffic light                          | 6       |
| traffic sign                           | 7       |
| vegetation                             | 8       |
| terrain                                | 9       |
| sky                                    | 10      |
| person                                 | 11      |
| rider                                  | 12      |
| car                                    | 13      |
| truck                                  | 14      |
| bus                                    | 15      |
| train                                  | 16      |
| motorcycle                             | 17      |
| bicycle                                | 18      |
| bear deer cow                          | 19      |
| garbage_bag stand_food trash_can       | 20      |

## Monocular depth estimation

### Evaluation metrics
See folder `./evaluation_depth/`. We provide two scripts, `./evaluation_depth/depth_metrics.py` is for depth prediction performance, and `./evaluation_depth/sparsification.py` is for sparsification curves and its corresponding uncertainty estimation performance metrics, more details on this mretric can be found in [this](https://openaccess.thecvf.com/content_CVPR_2020/html/Poggi_On_the_Uncertainty_of_Self-Supervised_Monocular_Depth_Estimation_CVPR_2020_paper.html) CVPR 2020 paper by Poggi et al..

### More information
The depth groundtruth data is in the form of `.exr` files. The depth in the image is annotated as min/max depth value. To load and transfer the depth in the image to the depth in meters, you can try the following codes:
```python
import cv2
from PIL import Image
import numpy as np
depth_path = 'xxx.exr'
depth = cv2.imread(depth_path, cv2.IMREAD_ANYCOLOR | cv2.IMREAD_ANYDEPTH)
depth = Image.fromarray(depth)
depth = np.asarray(depth, dtype=np.float32)
depth = 400 * (1 - depth) # the depth in meters
```

## Object tracking
TODO

## Citation
If you find this work useful for your research, please consider citing our paper:
```
@article{franchi2022muad,
  title={MUAD: Multiple Uncertainties for Autonomous Driving, a benchmark for multiple uncertainty types and tasks},
  author={Franchi, Gianni and Yu, Xuanlong and Bursuc, Andrei and Tena, Angel and Kazmierczak, R{\'e}mi and Dubuisson, S{\'e}verine and Aldea, Emanuel and Filliat, David},
  journal={arXiv preprint arXiv:2203.01437},
  year={2022}
}
```