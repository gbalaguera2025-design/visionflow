# Problem & Motivation

## Real-World Problem

Urban roads and highways are getting more congested every year.  
Cities install fixed traffic cameras, but most of the time those cameras are just **recording video** with no automatic understanding of what’s happening.

Human operators can’t watch every camera 24/7, so:

- Traffic jams can build up before anyone notices.
- Accidents or blocked lanes may not be detected quickly.
- There’s no easy way to measure *how often* certain roads are congested.

## VisionFlow Goal

**VisionFlow** uses a convolutional neural network (AlexNet) to classify camera images into:

- 🟥 **Traffic** – heavy or moderate congestion
- 🟩 **No Traffic** – light traffic / mostly clear road

This is a **binary classification** problem: given a single image, predict whether the scene shows traffic or not.

## Why This Matters

If this kind of model works well, it could help:

- 🏙️ **Smart cities**: automatic monitoring of traffic cameras in real time  
- 🚑 **Faster response**: quickly flag frames where there is likely congestion or an incident  
- 📊 **Better analytics**: estimate how often particular intersections are congested over time  
- 🌱 **Environment**: less time in stop-and-go traffic = lower emissions

## Dataset Used

For this project, I created a small custom dataset with two folders:

- `traffic/` – images that clearly show many cars / congestion
- `no_traffic/` – images where the road is relatively empty

The dataset is stored in Google Drive and loaded into Colab with PyTorch’s `ImageFolder`:

- **Classes:** `traffic`, `no_traffic`  
- **Train images:** ~160  
- **Validation images:** ~40  

Even though this is a small dataset, it’s enough to:

- Train a working AlexNet classifier  
- Run experiments with batch size, learning rate, and augmentation  
- Compare AlexNet to another architecture (e.g., ResNet18)
