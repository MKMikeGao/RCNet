# 'RCNet'(Refine-CornerNet)
This is object detection project.　　<br/>
Contact: [mikegao0415@gmail.com](mailto:mikegao0415@gmail.com). Any questions or discussions are welcomed! 

## Abstract
In object detection, keypoint-based approacheseliminate the need for designing a set of anchor boxes andachieved state-of-the-art accuracy of one-stage approaches.However, it often suffer unable trade-offs inference time andaccuracy, arguably due to the complexity of network frame-works. In this paper, we tackle the problem of keypoint-basedobject detection and introduce RCNet. We detect one key-point (center point), rather than a pair, which lead to improveeffectiveness in inference. In further, we redesigned key-point estimation network for stack hourglass network, namedRefine-hourglass. Without bells and whistles, we evaluateon MS-COCO dataset, RCNet achieves 44.6% AP at 32ms.The experiment result demonstrates our RCNet achieves thebest speed-accuracy trade-offs when compared with otherone-stage approaches.

## Object Detection on COCO validatio
| Backbone         |  AP / FPS | Flip AP / FPS|  Multi-scale AP / FPS |
|------------------|-----------|--------------|-----------------------|
|Refine-Hourglass  | 44.6 / 29 | 45.4 / 15    |       46.0 / 4        |

## Installation

Please refer to [INSTALL.md](readme/INSTALL.md) for installation instructions.

## Training RCNet
