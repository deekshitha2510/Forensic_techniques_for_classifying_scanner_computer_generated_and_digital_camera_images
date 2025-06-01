# Forensic_techniques_for_classifying_scanner_computer_generated_and_digital_camera_images
## 🔍 Overview

This project implements a **unified image source classification system** that determines whether an image originates from:
- A **digital camera**
- A **scanner**, or
- **Computer-generated (CG) software**

It leverages **sensor pattern noise** to distinguish between these sources in a **content-independent** and **orientation-invariant** manner.

## 🎯 Problem Statement
Digital imaging devices like cameras, scanners, and CG software generate images through different mechanisms, which influences the residual noise present in the images. The task is to **classify an image's origin** reliably for forensic analysis, without prior knowledge of the device type.

## 🚧 Forensic Challenges

- Identifying if an image is from a **camera, scanner, or CG software**
- Determining authenticity and **chain of custody** for legal evidence
- Dealing with **CG images** that lack sensor noise
- Existing methods require **pre-knowledge** of device class

## 💡 Proposed Solution
We propose a **feature-based classification method** that:

- Extracts **residual noise** using wavelet denoising (green channel only for efficiency)
- Computes **15 statistical features**
- Trains an **SVM classifier with RBF kernel** to classify image sources

### Key Advantages
- Independent of image content
- Robust to image orientation
- Doesn't require device type as prior input
### 📐 Mathematical Foundations

- Input image \( I \)
- Apply **wavelet denoising**
- Compute **residual noise** \( R = I - \text{denoised}(I) \)

### ✨ Feature Set Includes:

- **Row and column averages** of residual noise
- **Correlation features** (to identify periodic patterns from scanners)
- **Noise statistics** (standard deviation, kurtosis, etc.)

### 🔧 Implementation

- Use **only the green channel** to reduce computational load
- Preprocessing with `SimpleImputer` to handle missing values
- Images cropped to **1024×768**
- **SVM** classifier with hyperparameter tuning:
  - `C ∈ {1, 10, 100}`
  - `γ ∈ {0.01, 0.001, 0.0001}`

## 🛠 Enhancements Over Literature

- Structured output folders: cropped images, feature vectors, confusion matrix
- Error handling for incomplete or noisy data
- Tested all **RGB channels** for computational trade-offs
- Practical output saving for reproducibility

## 📊 Results

- Achieved **81% accuracy** (vs. paper's 91.5%)
- Precision, Recall, F1-score: **0.81**
- Balanced performance across CG and Camera images
- Paper's JPEG Q=90 result: **79.8%** (comparable to our performance)

### 🧪 Confusion Matrix

- Saved as a percentage-based matrix for clarity
- Helps visualize misclassifications effectively

## Key libraries used:

NumPy, OpenCV, Scikit-learn, PyWavelets, Matplotlib

## 📂 **Dataset**
- **Source**: [Dresden Image Database](https://www.kaggle.com/datasets/micscodes/dresden-image-database?resource)

## 📥 **Installation**

1. Clone the repository:

   git clone https://github.com/deekshitha2510/Forensic_techniques_for_classifying_scanner_computer_generated_and_digital_camera_images
