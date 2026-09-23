# Drone-Based Crop and Weed Detection

An ongoing computer vision project focused on detecting crops and weeds from aerial/drone imagery using a pretrained YOLO object detection model.

The project explores the use of deep learning for potential UAV-based agricultural applications, with a focus on model training, evaluation, error analysis, and improving dataset quality.

> **Project Status:** 🚧 Ongoing

---

## Overview

Agricultural fields can contain both crops and unwanted weeds. Detecting these objects from aerial imagery can support agricultural monitoring and potential precision agriculture applications.

In this project, a pretrained YOLO model is fine-tuned to detect two object classes from aerial imagery:

* **Crop**
* **Weed**

The current work includes training a baseline model, running predictions on test images, evaluating detection performance, and investigating prediction errors and possible missing annotations.

---

## Objectives

The main objectives of this project are to:

* Learn the fundamentals of YOLO-based object detection.
* Understand how pretrained deep learning models can be fine-tuned for a specific task.
* Train a YOLO model on a crop and weed aerial imagery dataset.
* Understand object detection metrics such as:

  * Precision
  * Recall
  * IoU
  * AP
  * mAP
* Run inference on unseen test images.
* Analyze false positive and false negative detections.
* Investigate possible missing annotations in the dataset.
* Explore methods for improving model performance.
* Develop practical computer vision experience relevant to UAV applications.

---

## Dataset

This project uses the **Weed Crop Aerial Dataset** from Roboflow Universe.

**Dataset:**
https://universe.roboflow.com/roboflow-100/weed-crop-aerial

**License:** CC BY 4.0

The dataset contains two object classes:

| Class ID | Class |
| -------- | ----- |
| 0        | Crop  |
| 1        | Weed  |

### Dataset Split

| Split      | Number of Images |
| ---------- | ---------------: |
| Training   |              823 |
| Validation |              235 |
| Test       |              118 |
| **Total**  |        **1,176** |

The dataset uses the YOLO annotation format.

Each annotation follows:

```text
class_id x_center y_center width height
```

The coordinates are normalized relative to the image dimensions.

---

## Model

A pretrained YOLO model is used as the starting point and fine-tuned on the crop and weed dataset.

The general workflow is:

```text
Pretrained YOLO Model
        ↓
Crop/Weed Dataset
        ↓
Fine-tuning
        ↓
Trained Model
        ↓
Validation & Testing
        ↓
Error Analysis
```

The model is trained to detect:

* Crop
* Weed

---

## Training

The model was trained using the Ultralytics YOLO framework.

Example training code:

```python
from ultralytics import YOLO

# Load a pretrained YOLO model
model = YOLO("yolo26n.pt")

# Fine-tune the model on the crop/weed dataset
results = model.train(
    data="dataset/data.yaml",
    epochs=30,
    imgsz=640,
    batch=8,
    name="crop_weed_detection"
)
```

The training process uses the pretrained model weights as the starting point rather than training the network entirely from random initialization.

---

## Prediction / Inference

After training, the resulting `best.pt` weights can be used to perform inference on test images.

Example:

```python
from ultralytics import YOLO

# Load the trained crop/weed model
model = YOLO(
    r"runs\detect\crop_weed_detection\weights\best.pt"
)

# Run the model on a test image
results = model.predict(
    source=r"path\to\test\image.jpg",
    conf=0.50,
    save=True
)

print("Prediction completed.")
```

The model produces bounding boxes, predicted classes, and confidence scores for detected objects.

---

## Model Evaluation

Model evaluation is being performed using object detection metrics including:

* Precision
* Recall
* IoU
* mAP@50
* mAP@50-95

These metrics are used to understand how accurately the model detects and localizes crops and weeds.

---

## Error Analysis

Rather than evaluating the model only using numerical metrics, prediction errors are also being investigated visually.

The analysis includes:

### False Positives

Cases where the model predicts an object as a weed when the prediction does not correspond to a weed in the ground-truth annotation.

### False Negatives

Cases where a weed is present in the image but the model fails to detect it.

### IoU Analysis

Intersection over Union (IoU) is used to compare predicted bounding boxes with ground-truth bounding boxes.

### Confidence Analysis

Prediction confidence scores are also examined to understand how confident the model is when making detections.

---

## Missing Annotation Investigation

During validation analysis, some predictions were found in regions that appeared to contain weeds but did not have corresponding ground-truth annotations.

A separate analysis was performed to identify images that may contain potentially missing weed annotations.

The automatically identified regions are treated only as **candidate missing annotations** and are manually inspected before modifying the dataset.

This process is intended to distinguish between:

```text
Model error
    vs.
Missing ground-truth annotation
```

The dataset correction and retraining process is currently ongoing.

---

## Project Workflow

The current workflow is:

```text
Dataset
   ↓
Dataset inspection
   ↓
Pretrained YOLO model
   ↓
Fine-tuning
   ↓
Validation
   ↓
Test predictions
   ↓
Error analysis
   ↓
Investigation of possible missing annotations
   ↓
Manual annotation verification
   ↓
Dataset improvement
   ↓

```

---

## Technologies Used

* **Python**
* **Ultralytics YOLO**
* **PyTorch**
* **OpenCV**
* **NumPy**
* **Matplotlib**
* **Roboflow Dataset**
* **Git / GitHub**

---
## Future Work

Possible future improvements include:

* Correcting verified missing annotations.
* Retraining the model using the improved dataset.
* Comparing baseline and improved model performance.
* Investigating false positive weed detections.
* Testing different YOLO model sizes.
* Exploring performance for small weed objects.
* Testing the model under different aerial imaging conditions.
* Exploring deployment possibilities for UAV-based agricultural monitoring.

---

## Disclaimer

This project is primarily a learning and experimentation project focused on understanding the practical workflow of computer vision and object detection.

The current model is not intended to be used as a production agricultural system.
