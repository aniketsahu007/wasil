# 🚀 Semantic Segmentation for Multi-Class Scene Understanding

## 🧠 Problem Statement

This project focuses on multi-class semantic segmentation.  
The goal is to assign each pixel in an image to one of 6 semantic classes.

Evaluation Metric:
- **Mean Intersection over Union (mIoU)**

IoU is used because pixel accuracy is not sufficient for segmentation quality evaluation.

---

## 📂 Dataset Description

The dataset consists of:

- Training images
- Training masks
- Validation images
- Validation masks

Each mask contains 6 semantic classes represented by the following original labels:

| Original Label | Remapped Label |
|---------------|---------------|
| 0             | 0             |
| 1             | 1             |
| 2             | 2             |
| 3             | 3             |
| 27            | 4             |
| 39            | 5             |

All masks are remapped to values in range `[0–5]` for model compatibility.

---

## 🛠️ Data Preprocessing

1. Images resized to **512×512**
2. Masks resized using **Nearest Neighbor interpolation**
3. Pixel values normalized to `[0,1]`
4. Masks converted to `LongTensor`
5. Data augmentation:
   - Random horizontal flip (50% probability)

These steps ensure training stability and improve generalization.

---

## 🏗️ Model Architecture

The model used is a custom **U-Net** architecture.

### Why U-Net?

- Encoder–Decoder structure
- Skip connections for spatial detail retention
- Efficient for pixel-level segmentation tasks
- Performs well with moderate dataset sizes

### Architecture Overview:

Encoder:
- 3 Downsampling blocks
- Convolution + ReLU layers
- MaxPooling for feature extraction

Bottleneck:
- Deep feature representation

Decoder:
- Transposed Convolutions (Upsampling)
- Skip connections from encoder
- Feature fusion

Final Layer:
- 1×1 Convolution
- Outputs 6 class channels

---

## 🎯 Loss Function

To directly optimize segmentation quality, we use:

### 1️⃣ CrossEntropy Loss
Handles multi-class pixel classification.

### 2️⃣ Dice Loss
Improves region overlap and directly enhances IoU performance.

### Final Loss:
Total Loss = CrossEntropy + 0.5 × DiceLoss
