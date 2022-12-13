# **딥러닝 응용II:컴퓨터비전 최종 프로젝트**



## Solving Inefficiency of Self-supervised Representation Learning 재현

Paper link: [https://arxiv.org/abs/2104.08760](https://arxiv.org/abs/2104.08760)

Github link: https://github.com/parkjungha/triplet




1. **Download the pretrained model.**   
- Source (provided by authors):

| Model | Top 1 Acc | Download |
| --- | --- | --- |
| shorter epochs | 73.8% | ⬇️ |
| longer epochs | 75.9% | ⬇️ |

I use the longer epochs one because of the better performance.      




2. **Download the dataset.**  
- Source: [https://cocodataset.org/](https://cocodataset.org/)

I use [2017 Train images [118K/18GB]](http://images.cocodataset.org/zips/train2017.zip) and [2017 Train/Val annotations [241MB]](http://images.cocodataset.org/annotations/annotations_trainval2017.zip).

and put them to `triplet/benchmarks/detection/datasets/coco` directory.      





3. **Install required libraries.**   
- [OpenSelfSup](https://github.com/open-mmlab/OpenSelfSup)
- [detectron2](https://github.com/facebookresearch/detectron2)

This repo is a modification on the OpenSelfSup.

For object detection and instance segmentation tasks, this repo follows OpenSelfSup and uses Detectron2.      




4. **Train the model.**   

```bash
python convert-pretrain-to-detectron2.py  ~/triplet/pretrained/release_ep940.pth  ~/triplet/pretrained/output_detection_ep940.pkl

bash [run.sh](http://run.sh/) configs/coco_R_50_C4_2x_moco.yaml ~/triplet/pretrained/output_detection_ep940.pkl
```



      
5. **Evaluate the performance.**   

This is the reported performances by authors.

| Method | AP(box) | AP(mask) |
| --- | --- | --- |
| supervised | 40.0 | 34.7 |
| Random | 35.6 | 31.4 |
| Relative-Loc | 40.0 | 35.0 |
| Rotation-Pred | 40.0 | 34.9 |
| NPID | 39.4 | 34.5 |
| SimCLR | 39.6 | 34.6 |
| MoCo | 40.9 | 35.5 |
| MoCo v2 | 40.9 | 35.5 |
| BYOL | 40.3 | 35.1 |
| Triplet | 41.7 | 36.2 |

However, in my case, the results are **AP(box) = 25.1 and AP(mask) = 22.3.**

This results are quite lower than the reported values, I think this is because the insufficient training epochs are set due to the limited computing resources in my environment.      
