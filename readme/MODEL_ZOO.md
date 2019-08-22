# MODEL ZOO

### Common settings and notes

- The experiments are run with pytorch 0.4.1, CUDA 9.0, and CUDNN 7.1.
- Testing times are measured on our local machine with NVIDIA 1070Ti GPU. 

## Object Detection


### COCO

| Model                    | GPUs |Train time(h)| Test time (ms) |   AP               |  Download | 
|--------------------------|------|-------------|----------------|--------------------|-----------|
|[ctdet\_coco\_hg](../experiments/ctdet_coco_hg.sh)       |   5  |109          | 71 / 129 / 674 | 40.3 / 42.2 / 45.1 | [model](https://drive.google.com/open?id=1cNyDmyorOduMRsgXoUnuyUiF6tZNFxaG) |
#### Notes

- All models are trained on COCO train 2017 and evaluated on val 2017. 
- We show test time and AP with no augmentation / flip augmentation / multi scale (0.5, 0.75, 1, 1.25, 1.5) augmentation. 
- Results on COCO test-dev can be found in the paper or add `--trainval` for `test.py`. 
- exdet is our re-implementation of [ExtremeNet](https://github.com/xingyizhou/ExtremeNet). The testing does not include edge aggregation.
- For dla and resnets, `1x` means the training schedule that train 140 epochs with learning rate dropped 10 times at the 90 and 120 epoch (following [SimpleBaseline](https://github.com/Microsoft/human-pose-estimation.pytorch)). `2x` means train 230 epochs with learning rate dropped 10 times at the 180 and 210 epoch. The training schedules are **not** carefully investigated.
- The hourglass trained schedule follows [ExtremeNet](https://github.com/xingyizhou/ExtremeNet): trains 50 epochs (approximately 250000 iterations in batch size 24) and drops learning rate at the 40 epoch.
- Testing time include network forwarding time, decoding time, and nms time (for ExtremeNet).
- We observed up to 0.4 AP performance jitter due to randomness in training. 
