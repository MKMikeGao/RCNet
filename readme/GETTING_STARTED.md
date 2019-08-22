# Getting Started

This document provides tutorials to train and evaluate CenterNet. Before getting started, make sure you have finished [installation](INSTALL.md) and [dataset setup](DATA.md).

## Benchmark evaluation

First, download the models you want to evaluate from CenterNet [model zoo](MODEL_ZOO.md) and put them in `CenterNet_ROOT/models/`. 

### COCO

To evaluate COCO object detection with DLA
run

~~~
python test.py ctdet --exp_id coco_hg --keep_res --load_model ../models/ctdet_coco_hg.pth
~~~

This will give an AP of `37.4` if setup correctly. `--keep_res` is for keep the original image resolution. Without `--keep_res` it will resize the images to `512 x 512`. You can add `--flip_test` and `--flip_test --test_scales 0.5,0.75,1,1.25,1.5` to the above commend, for flip test and multi_scale test, respectively. The expected APs are `39.2` and `41.7`, respectively.

To test with hourglass net, run

~~~
python test.py ctdet --exp_id coco_hg --arch hourglass --fix_res --load_model ../models/ctdet_coco_hg.pth
~~~

The expected results can be found in the model zoo.

## Training

We have packed all the training scripts in the [experiments](../experiments) folder.
The experiment names are correspond to the model name in the [model zoo](MODEL_ZOO.md).
The number of GPUs for each experiments can be found in the scripts and the model zoo.
In the case that you don't have 8 GPUs, you can follow the [linear learning rate rule](https://arxiv.org/abs/1706.02677) to scale the learning rate as batch size.
For example, to train COCO object detection with dla on 1 GPUs, run

~~~
python main.py ctdet --exp_id coco_hg --batch_size 2 --master_batch 15 --lr 1.25e-4  --gpus 0
~~~

The default learning rate is `1.25e-4` for batch size `2` (on 1 GPUs for NVIDIA 1070Ti).
By default, pytorch evenly splits the total batch size to each GPUs.
`--master_batch` allows using different batchsize for the master GPU, which usually costs more memory than other GPUs.
If it encounters GPU memory out, using slightly less batch size (e.g., `112` of `128`) with the same learning is fine.

If the training is terminated before finishing, you can use the same commond with `--resume` to resume training. It will found the lastest model with the same `exp_id`.

Our HourglassNet model is finetuned from the pretrained [ExtremeNet model](https://drive.google.com/file/d/1omiOUjWCrFbTJREypuZaODu0bOlF_7Fg/view?usp=sharing) (from the [ExtremeNet repo](https://github.com/xingyizhou/ExtremeNet)).
You will need to download the model, run `python convert_hourglass_weight.py` to convert the model format, and load the model for training (see the [script](../experiments/ctdet_coco_hg.sh)).
