# Semantic Segmentation on Cityscapes Dataset 


## 🧠 Introduction

Semantic segmentation is a key task in computer vision that involves classifying every pixel in an image into predefined categories. It's widely used in:
- **Autonomous driving** (e.g., identifying roads, vehicles, pedestrians)
- **Medical imaging** (e.g., tumor detection)
- **Urban scene understanding**

This project uses the **Cityscapes dataset**, which contains 5000 finely annotated urban street scene images. Due to limited access to test images, **validation accuracy** is the main performance metric.

---

## 🧩 Project Overview

Our approach consisted of the following key steps:

1. 📊 **Dataset Analysis** – Understanding Cityscapes format and valid classes  
2. 🧼 **Preprocessing** – Image resizing, encoding masks, color remapping  
3. 🖼️ **Visualization** – Input images and corresponding masks  
4. 🏗️ **Model Development** – Trying various architectures  
5. 🎯 **Loss Functions** – Experimenting with standard and custom ones  
6. 🧪 **Post-Processing** – Applying CRF (Conditional Random Fields)  
7. 📉 **Evaluation** – Using validation accuracy and IOU  

---

## 🛠️ Approaches & Architectures

### 1. 🧬 UNet (Baseline)
- Basic encoder-decoder with skip connections
- Input Size: `256x256`
- **Accuracy**: `83.80%`
- Used primarily to validate preprocessing pipeline

---

### 2. 🧠 DeepLabV3+ (Best Performing)
- Backbone: `ResNet-50 pretrained on ImageNet`
- Concepts: `Atrous Convolution`, `ASPP`
- Input Size: `256x512`
- **Accuracy**: `87.29%`
- Custom loss with Sobel edge filter
- Tried CRF post-processing (minimal improvement)

---

### 3. 🔍 Attention ResUNet
- Introduced attention gates and residual connections
- Input Size: `128x128`
- **Accuracy**: `82.40%`
- Attention helped focus on spatially important regions

---

### 4. 🌐 PSPNet
- Used Pyramid Pooling for global + local context
- Input Size: `128x128`
- **Accuracy**: `82.10%`

---

### 5. 🦾 YOLOv8 (Detection-based Attempt)
- Attempted object detection on Cityscapes
- Objective: Fine-tune for semantic regions like sky, road, buildings
- **Result**: Limited success due to incomplete fine-tuning

---

## ⛔ Blockers Faced

- ❌ GPU crashes on higher input resolutions
- ⚠️ Directory mismatches and shape errors in training
- ⚙️ Debugging preprocessing pipelines and label encoding
- 🧮 Required one-hot encoding + categorical cross-entropy in some models

---

## 📊 Results Summary

| S. No | Model                   | Input Resolution | Validation Accuracy |
|-------|-------------------------|------------------|---------------------|
| 1     | PSPNet                  | 128x128          | 82.10%              |
| 2     | Attention ResUNet       | 128x128          | 82.40%              |
| 3     | Basic UNET              | 256x256          | 83.80%              |
| 4     | DeepLabV3+              | 256x512          | 87.16%              |
| 5     | DeepLabV3+ (Custom Loss)| 256x512          | **87.29%**          |

---

## 🚀 Future Work

- 📈 **Data Augmentation** to enrich training samples  
- 🔍 **Higher input resolutions** for sharper segmentations  
- 📐 **Optimizing IOU/Jaccard scores** directly as training objectives  
- 🧩 Try **Dice / Tversky / Focal / Lovasz** losses  
- 🔁 **Improved dilation schemes** for broader receptive fields  
- 📦 **Complete YOLO finetuning** for semantic regions  

---

## 📁 Dataset

- Source: [Cityscapes Dataset](https://www.cityscapes-dataset.com/)
- Used: `gtFine` (masks) and `leftImg8bit` (images)
- Test set not accessible → **Validation set used exclusively**

---

## 📷 Sample Outputs

Visual comparisons between ground truth and predicted masks are available in the project folder. UNet and DeepLab outputs show clear pixel-wise labeling, with DeepLab producing the sharpest segmentations.

---

## 📚 References

- [UNet](https://arxiv.org/abs/1505.04597)  
- [DeepLabV3+](https://arxiv.org/abs/1802.02611)  
- [Attention UNet](https://arxiv.org/abs/1804.03999)  
- [PSPNet](https://arxiv.org/abs/1612.01105)  
- [YOLOv8](https://github.com/ultralytics/ultralytics)


