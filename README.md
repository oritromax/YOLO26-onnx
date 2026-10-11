# YOLO26 ONNX Export

YOLO26 Model exported for ONNX usage in Frigate.

[Model Reference](https://docs.ultralytics.com/models/yolo26)

[Frigate Object Detectors](https://docs.frigate.video/configuration/object_detectors)

Frigate doesn't officially support YOLO26 yet. The default export uses the NMS-free head (`[1, 300, 6]` output), which Frigate can't parse, so these models are exported with `end2end=False` to get the classic `[1, 84, 8400]` output that Frigate's `yolo-generic` model type understands.

| Model | Test Size | mAP<sup>val</sup> 50-95 | T4 TensorRT10 | Param. | FLOPs | Exported |
| :-- | :-: | :-: | :-: | :-: | :-: | :-: |
| [**YOLO26-N**] | 640 | **40.9%** | **1.7 ms** | **2.4M** | **5.5G** | [ ] |
| [**YOLO26-S**] | 640 | **48.6%** | **2.5 ms** | **9.5M** | **20.9G** | [ ] |
| [**YOLO26-M**] | 640 | **53.1%** | **4.7 ms** | **20.4M** | **68.4G** | [ ] |
| [**YOLO26-L**] | 640 | **55.0%** | **6.2 ms** | **24.8M** | **86.8G** | [ ] |
| [**YOLO26-X**] | 640 | **57.5%** | **11.8 ms** | **55.7M** | **194.4G** | [ ] |

YOLO26 weights are licensed under AGPL-3.0 by Ultralytics, so this repository is AGPL-3.0 as well.
