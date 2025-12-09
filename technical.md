# Technical Approach – AlexNet & Training Setup

## Model: AlexNet

I use a convolutional neural network based on **AlexNet**, adapted for a 2-class problem.

### Architecture (high level)

- **Input:** 3-channel RGB image, resized to **224 × 224**
- **Convolution + ReLU + MaxPool layers**
  - multiple conv layers extract edges, textures, shapes and patterns
  - pooling layers downsample the feature maps and add translation invariance
- **Fully connected layers**
  - flatten the feature maps into a vector
  - two or three dense layers with ReLU activations
- **Output layer**
  - final linear layer with **2 outputs** (for `traffic` and `no_traffic`)
  - followed by **softmax** during evaluation to get class probabilities

In PyTorch, I start from a pre-trained `torchvision.models.alexnet` and replace the final classifier layer with a `Linear(..., 2)` for my two classes.

---

## Data Pre-Processing

### Image pipeline

All images go through the following steps:

1. **Resize** to `224 × 224`
2. **Convert to tensor**
3. **Normalize** pixel values using ImageNet-style mean and std, e.g.  
   `mean = [0.485, 0.456, 0.406]`  
   `std  = [0.229, 0.224, 0.225]`

### Data augmentation

To make the model more robust, I also use augmentation (for the “with augmentation” runs):

- Random horizontal flips  
- Small random rotations  
- Minor color jitter (brightness / contrast)

These augmentations are only applied to the **training** set, not the validation set.

---

## Training Setup

- **Framework:** PyTorch in Google Colab  
- **Loss function:** Cross-Entropy Loss (for multi-class classification)  
- **Optimizer:** Adam (or SGD with momentum)  
- **Base learning rate:** `1e-3` (0.001) for the baseline  
- **Batch sizes:** 16, 32, 64 in different experiments  
- **Epochs:** around 5–10 (longer runs possible if needed)  
- **Train/Val split:** about 80% train, 20% validation

During training I track:

- **Training loss & accuracy** per epoch  
- **Validation loss & accuracy** per epoch  

using both console output and **Weights & Biases (wandb)**.

---

## Experiments Implemented

In the Colab notebook I run several experiments:

1. **Baseline AlexNet**
   - batch size = 32  
   - learning rate = 1e-3  
   - with data augmentation

2. **Batch size comparison**
   - AlexNet with batch sizes **16** and **64**  
   - compare speed of convergence and stability of validation accuracy

3. **Learning rate comparison**
   - learning rates **1e-3** vs **1e-4**  
   - see how too small LR can slow learning and too large can be unstable

4. **Augmentation ON vs OFF**
   - same hyperparameters, but one run with augmentation disabled  
   - compare overfitting and validation performance

5. **Architecture comparison**
   - AlexNet vs **ResNet18**  
   - both trained on the same dataset and logged to wandb

Details (metrics and plots) are summarized on the **Experiments & Results** page.
