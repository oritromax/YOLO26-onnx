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
| [**YOLO26-N**](yolo26-n-320.onnx) | 320 | **2.4M** | **~1.4G** | ✅ | ✅ |
| [**YOLO26-S**](yolo26-s-320.onnx) | 320 | **9.5M** | **~5.2G** | ✅ | ✅ |
| [**YOLO26-M**](yolo26-m-320.onnx) | 320 | **20.4M** | **~17.1G** | ✅ | ✅ |
| [**YOLO26-L**](yolo26-l-320.onnx) | 320 | **24.8M** | **~21.7G** | ✅ | ✅ |
| [**YOLO26-X**](https://github.com/oritromax/YOLO26-onnx/releases/tag/yolo26-x-320) | 320 | **55.7M** | **~48.6G** | ✅ | ✅ |

## 640

| Model | Test Size | mAP<sup>val</sup> 50-95 | T4 TensorRT10 | Param. | FLOPs | Exported | Tested |
| :-- | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| [**YOLO26-N**](yolo26-n-640.onnx) | 640 | **40.9%** | **1.7 ms** | **2.4M** | **5.5G** | ✅ | ✅ |
| [**YOLO26-S**](yolo26-s-640.onnx) | 640 | **48.6%** | **2.5 ms** | **9.5M** | **20.9G** | ✅ | ✅ |
| [**YOLO26-M**](yolo26-m-640.onnx) | 640 | **53.1%** | **4.7 ms** | **20.4M** | **68.4G** | ✅ | ✅ |
| [**YOLO26-L**](yolo26-l-640.onnx) | 640 | **55.0%** | **6.2 ms** | **24.8M** | **86.8G** | ✅ | ✅ |
| [**YOLO26-X**](https://github.com/oritromax/YOLO26-onnx/releases/tag/yolo26-x-640) | 640 | **57.5%** | **11.8 ms** | **55.7M** | **194.4G** | ✅ | ✅ |

## Test results

Tested in Frigate 0.17.1 (`-tensorrt` image, `onnx` detector on CUDA, RTX 2080 Ti), `yolo-generic`, against a 70 s indoor recording with three people in frame, looped at detect 1280x720 @ 5 fps. Every model loaded, created person events, and kept every score within 0 to 1. YOLOv9-S is included as the baseline.

| Model | Size | Run | Frigate inference | Person events | Avg top score | Max top score |
| :-- | :-: | :-: | :-: | :-: | :-: | :-: |
| YOLO26-N | 320 | 150 s | 4.1 ms | 6 | 0.84 | 0.90 |
| YOLO26-N | 640 | 150 s | 13.9 ms | 8 | 0.81 | 0.89 |
| YOLO26-S | 320 | 240 s | 5.3 ms | 9 | 0.86 | 0.93 |
| YOLO26-S | 640 | 240 s | 14.3 ms | 13 | 0.84 | 0.91 |
| YOLO26-M | 320 | 150 s | 7.8 ms | 6 | 0.84 | 0.94 |
| YOLO26-M | 640 | 150 s | 16.3 ms | 7 | 0.85 | 0.94 |
| YOLO26-L | 320 | 150 s | 9.7 ms | 5 | 0.87 | 0.94 |
| YOLO26-L | 640 | 150 s | 24.0 ms | 6 | 0.86 | 0.94 |
| YOLO26-X | 320 | 150 s | 17.0 ms | 4 | 0.92 | 0.94 |
| YOLO26-X | 640 | 150 s | 28.1 ms | 4 | 0.92 | 0.95 |
| *YOLOv9-S (baseline)* | *640* | *240 s* | *16.3 ms* | *10* | *0.90* | *0.93* |

Event counts depend on run length (the clip loops), so compare them only between rows with the same Run time.

The X models are over GitHub's 100 MB per-file limit, so they are release downloads instead of repo files.

YOLO26 weights are licensed under AGPL-3.0 by Ultralytics, so this repository is AGPL-3.0 as well.
