# FastMVS experiments

This is a modified version of Fast-MVSNet for Deep Learning course project 2020.

Based on CVPR 2020 paper:

[Fast-MVSNet: Sparse-to-Dense Multi-View Stereo With Learned Propagation and Gauss-Newton Refinement](https://arxiv.org/pdf/2003.13017.pdf)


## How to use
```bash
git clone https://github.com/ohrmuzd/FastMVS_experiments
```
### Installation
 ```bash
pip install -r requirements.txt
```

### Training
* Download the preprocessed [DTU training data](https://drive.google.com/file/d/1eDjh-_bxKKnEuz5h-HXS7EDJn59clx6V/view) from [MVSNet](https://github.com/YoYo000/MVSNet) and unzip it to ```data/dtu```.
* Train the network


    ```python fastmvsnet/train.py --cfg configs/dtu.yaml``` - for original FastMVSNet


    ```python fastmvsnet/train1.py --cfg configs/dtu.yaml``` - for FastMVSNet with gt_depth directly added into the input as another dimension


    ```python fastmvsnet/train2.py --cfg configs/dtu.yaml``` - for FastMVSNet with gt_depth features extracted separately and concatenated to image features  
  
  
    You could change the batch size in the configuration file according to your own pc.

### Testing
* Download the [rectified images](http://roboimagedata2.compute.dtu.dk/data/MVS/Rectified.zip) from [DTU benchmark](http://roboimagedata.compute.dtu.dk/?page_id=36) and unzip it to ```data/dtu/Eval```.
    
* Test with the pretrained model

    ```python fastmvsnet/test.py --cfg configs/dtu.yaml TEST.WEIGHT outputs/pretrained.pth```

### Depth Fusion
We need to apply depth fusion ```tools/depthfusion.py``` to get the complete point cloud. Please refer to [MVSNet](https://github.com/YoYo000/MVSNet) for more details.

```bash
python tools/depthfusion.py -f dtu -n flow2
```
