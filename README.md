# Drone-Based Crop and Weed Detection

An ongoing computer vision project focused on detecting crops and weeds from aerial/drone imagery using YOLO-based object detection.

The project explores object detection for potential UAV-based agricultural applications, with a focus on understanding model training, evaluation, error analysis, and performance improvement.

> **Project Status:** 🚧 Ongoing

---

## Overview

Agricultural fields can contain both crops and unwanted weeds. Detecting these objects from aerial imagery can be useful for monitoring agricultural fields and supporting precision agriculture applications.

In this project, a YOLO-based object detection model is trained to distinguish between two classes:

- **Crop**
- **Weed**

The current work focuses on establishing a baseline model, evaluating its performance, analyzing its errors, and investigating possible approaches for improving detection performance.

---

## Objectives

The main objectives of this project are to:

- Learn the fundamentals of YOLO-based object detection.
- Train a pretrained YOLO model on a custom crop and weed dataset.
- Evaluate object detection performance using standard detection metrics.
- Understand precision, recall, IoU, AP, and mAP.
- Analyze false positives and false negatives.
- Investigate the causes of incorrect weed detections.
- Explore methods for improving model performance.
- Develop experience with computer vision for UAV and agricultural applications.

---

## Dataset
This project uses the Weed Crop Aerial dataset from Roboflow Universe.

Dataset:
https://universe.roboflow.com/roboflow-100/weed-crop-aerial

License: CC BY 4.0
The dataset contains two object classes:

| Class ID | Class |
|---:|---|
| 0 | Crop |
| 1 | Weed |

### Dataset Split

| Split | Number of Images |
|---|---:|
| Training | 823 |
| Validation | 235 |
| Test | 118 |
| **Total** | **1176** |

The dataset uses the YOLO annotation format.

Each annotation follows:

```text
class_id x_center y_center width height
