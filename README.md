# YOLO26 ONNX Export

YOLO26 Model exported for ONNX usage in Frigate.

[Model Reference](https://docs.ultralytics.com/models/yolo26)

[Frigate Object Detectors](https://docs.frigate.video/configuration/object_detectors)

Frigate doesn't officially support YOLO26 yet. The default export uses the NMS-free head (`[1, 300, 6]` output), which Frigate can't parse, so these models are exported with `end2end=False` to get the classic `[1, 84, N]` output that Frigate's `yolo-generic` model type understands.

Exported = ONNX built with `end2end=False` and output shape verified. Tested = loaded in Frigate and producing sane detections.

## 320

Upstream only publishes mAP at 640, so this table has no mAP columns. FLOPs are approximate (the 640 value ÷ 4).

| Model | Test Size | Param. | FLOPs | Exported | Tested |
| :-- | :-: | :-: | :-: | :-: | :-: |
| [**YOLO26-N**](yolo26-n-320.onnx) | 320 | **2.4M** | **~1.4G** | ✅ | ⬜ |
| [**YOLO26-S**](yolo26-s-320.onnx) | 320 | **9.5M** | **~5.2G** | ✅ | ⬜ |
| [**YOLO26-M**](yolo26-m-320.onnx) | 320 | **20.4M** | **~17.1G** | ✅ | ⬜ |
| [**YOLO26-L**](yolo26-l-320.onnx) | 320 | **24.8M** | **~21.7G** | ✅ | ⬜ |
| [**YOLO26-X**](https://github.com/oritromax/YOLO26-onnx/releases/tag/yolo26-x-320) | 320 | **55.7M** | **~48.6G** | ✅ | ⬜ |

## 640

| Model | Test Size | mAP<sup>val</sup> 50-95 | T4 TensorRT10 | Param. | FLOPs | Exported | Tested |
| :-- | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| [**YOLO26-N**](yolo26-n-640.onnx) | 640 | **40.9%** | **1.7 ms** | **2.4M** | **5.5G** | ✅ | ⬜ |
| [**YOLO26-S**](yolo26-s-640.onnx) | 640 | **48.6%** | **2.5 ms** | **9.5M** | **20.9G** | ✅ | ⬜ |
| [**YOLO26-M**](yolo26-m-640.onnx) | 640 | **53.1%** | **4.7 ms** | **20.4M** | **68.4G** | ✅ | ⬜ |
| [**YOLO26-L**](yolo26-l-640.onnx) | 640 | **55.0%** | **6.2 ms** | **24.8M** | **86.8G** | ✅ | ⬜ |
| [**YOLO26-X**](https://github.com/oritromax/YOLO26-onnx/releases/tag/yolo26-x-640) | 640 | **57.5%** | **11.8 ms** | **55.7M** | **194.4G** | ✅ | ⬜ |

The X models are over GitHub's 100 MB per-file limit, so they are release downloads instead of repo files.

YOLO26 weights are licensed under AGPL-3.0 by Ultralytics, so this repository is AGPL-3.0 as well.
