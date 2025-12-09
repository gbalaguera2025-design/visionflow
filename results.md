# Experiments & Results

This page summarizes my main experiments with AlexNet on the VisionFlow traffic dataset and shows how the model behaved during training.

---

## Baseline AlexNet Run

**Setup:**

- Model: AlexNet (pre-trained, final layer changed to 2 classes)
- Batch size: **32**
- Learning rate: **1e-3**
- Data augmentation: **ON**
- Epochs: **5**
- Tracking: **Weights & Biases** (wandb project: `visionflow-alexnet`)

**Observed performance (baseline):**

- Best **validation accuracy**: around **95%**
- Training accuracy improves steadily over the first few epochs
- Validation loss decreases overall, with a small bump near the end (normal for a small dataset)

---

## Training Curves (Baseline)

### Validation Loss

![Validation loss over epochs](https://raw.githubusercontent.com/gbalaguera2025-design/visionflow/main/Screenshot%202025-12-09%20014520.png)

- The validation loss generally trends downward.
- There is a dip around the middle epochs, showing the model is learning useful features.
- Small fluctuations near the end are expected with a small dataset.

### Validation Accuracy

![Validation accuracy over epochs](https://raw.githubusercontent.com/gbalaguera2025-design/visionflow/main/Screenshot%202025-12-09%20014544.png)

- Validation accuracy climbs from around ~50–60% up to the **90–95%** range.
- This shows the model is generalizing reasonably well to unseen images.

### Training Loss

![Training loss over epochs](https://raw.githubusercontent.com/gbalaguera2025-design/visionflow/main/Screenshot%202025-12-09%20014607.png)

- Training loss drops quickly in the first epoch.
- After that, it continues to decrease more slowly, which is a typical pattern.

### Training Accuracy

![Training accuracy over epochs](https://raw.githubusercontent.com/gbalaguera2025-design/visionflow/main/Screenshot%202025-12-09%20014630.png)

- Training accuracy steadily increases and stabilizes at a fairly high value.
- The gap between training and validation accuracy is not huge, so overfitting is limited but still possible (common with small datasets).

---

## Takeaways

- ✅ **AlexNet is able to learn the traffic vs no_traffic distinction well** on this dataset, reaching ~95% validation accuracy.
- ✅ **Data augmentation** helps the model generalize better by slightly reducing overfitting.
- 🔍 **Hyperparameters like batch size and learning rate** change how quickly and how smoothly the loss/accuracy curves evolve.
- 🧠 **More data** and longer training (more epochs) would likely give even more stable results and better performance.

---

## Links

- 📓 **Colab notebook (full code & experiments):**  
  *(insert your Colab link here)*

- 📈 **Weights & Biases project (all runs & interactive plots):**  
  https://wandb.ai/gbalaguera2025-florida-atlantic-university/visionflow-alexnet
