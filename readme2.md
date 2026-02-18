
This combination improves boundary prediction and class overlap accuracy.

---

## ⚙️ Optimization Strategy

- Optimizer: **AdamW**
- Initial Learning Rate: `1e-4`
- Learning Rate Scheduler: StepLR
  - Step size: 20 epochs
  - Gamma: 0.5
- Batch Size: 1
- Training Epochs: 60
- Best model saved based on **Validation IoU**

---

## 📏 Evaluation Metric

### Intersection over Union (IoU)
IoU = Intersection / Union



Where:

- Intersection = pixels correctly predicted for a class
- Union = total pixels predicted + ground truth pixels - intersection

Mean IoU (mIoU) is calculated across all 6 classes.

The best model is selected based on highest validation mIoU.

---

## 🖥️ Hardware Used

- GPU: NVIDIA RTX 3050 (Laptop)
- CUDA-enabled PyTorch

---

## 📈 Training Strategy

1. Stable pipeline setup
2. Class remapping verification
3. IoU metric implementation
4. Resume training capability
5. Data augmentation integration
6. Combined loss for better region overlap

---

## 🔥 Key Design Decisions

- Chose U-Net for reliable segmentation performance
- Combined Dice + CE to improve IoU directly
- Implemented scheduler to prevent plateau
- Saved best model based on validation IoU (not loss)

---

## 📊 Future Improvements

- Advanced augmentations (rotation, scaling, brightness)
- Larger backbone encoder
- Mixed precision training
- Ensemble models

---

## 🏆 Conclusion

This implementation provides:

- Stable training
- Competitive IoU optimization
- Clean architecture
- Reproducible pipeline
- Efficient GPU utilization

The system is designed to maximize validation IoU performance while maintaining training stability and interpretability.


For each class:

