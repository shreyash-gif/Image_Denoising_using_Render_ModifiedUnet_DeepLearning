# Image Denoising using Blender and Deep Learning

## Table of Contents
- [Introduction](#introduction)
- [Objective](#objective)
- [Dataset Preparation](#dataset-preparation)
- [Methodology](#methodology)
- [Model Architecture](#model-architecture)
- [Evaluation](#evaluation)
- [Applications](#applications)
- [Results](#results)
- [References](#references)
  
## Introduction
This project focuses on enhancing rendered images by reducing noise using a combination of Blender for dataset creation and a Modified U-Net architecture for denoising. The primary goal is to achieve high-quality image restoration through deep learning, targeting applications in gaming, medical imaging, astronomy, and security systems.



## Objective
The project aims to:
1. Develop a dataset using Blender by rendering 3D models at varying noise levels.
2. Build a robust Modified U-Net model for image denoising.
3. Implement advanced denoising strategies such as Grid-Based and Sliding Window approaches.
4. Evaluate the model's performance on metrics like MSE and SSIM.

## Dataset Preparation
- **Source**: Dataset created using Blender by rendering scenes with random objects, materials, and camera positions.
![Screenshot 2024-11-13 220836](https://github.com/user-attachments/assets/bc547325-1aa4-4edd-be04-dbcee6e2a963)
![Screenshot 2024-11-13 220859](https://github.com/user-attachments/assets/1437473a-c2d4-4c06-8979-457d672e2937)
![Screenshot 2024-11-13 220932](https://github.com/user-attachments/assets/f75975d9-df82-4fb2-9564-4d27bae8d4a6)

- **File Details**: `dataset2.zip`
  - Contains noisy images (`noise/`) and corresponding clean images (`denoise/`).
- **Processing**:
  - Images resized to `64x64x3` for consistency.
  - Normalized pixel values to `[0, 1]`.
    
    ![Screenshot 2024-11-14 012449](https://github.com/user-attachments/assets/f3ceb2b8-6b5e-4ba7-97ce-3f982bd07c02)

## Methodology
1. **Data Collection**:
   - Blender scripting API used to render noisy and clean images at different sample rates (e.g., 1spp for noisy and 1024spp for clean images).
2. **Data Loading**:
   - `DataLoader` for loading image pairs.
   - `RanCropDataLoader` for generating random patches for training.
3. **Training**:
   - Optimizer: Adam
   - Loss Function: Combined MSE and SSIM loss.
   - Batch Size: Configured for efficient training.
   - Epochs: 30 iterations.

## Model Architecture
- **Base Model**: Modified U-Net
  - **Encoder**: Captures hierarchical features with convolutional layers.
  - **Decoder**: Reconstructs denoised images with transposed convolutions.
  - **Skip Connections**: Preserve spatial details by concatenating encoder features with decoder activations.
  - **Output**: Sigmoid activation for pixel values in `[0, 1]`.

## Evaluation
- **Metrics**:
  - Mean Squared Error (MSE)
  - Structural Similarity Index Measure (SSIM)
    ![Evaluton_Metircs](https://github.com/user-attachments/assets/0ebbcc10-009b-49e6-bccb-2b733369ed8d)
- **Visualization**:
  - Plots comparing noisy, clean, and denoised images.

## Applications
1. **Medical Imaging**: Enhanced MRI, CT, and X-ray scans.
2. **Photography**: Improved quality in low-light conditions.
3. **Surveillance**: Better clarity in low-light footage.
4. **Astronomy**: Cleaning noisy astronomical images for better object detection.

## Results
- Implemented denoising strategies:
  1. **Grid-Based Denoising**: Processes images in non-overlapping patches.
  2. **Sliding Window Denoising**: Uses overlapping patches to reduce boundary artifacts.
- Demonstrated high-quality denoising results through visual comparisons and quantitative metrics.
![img10grid](https://github.com/user-attachments/assets/b4057e10-41ac-41dd-bb01-8f166aabea1b)
Grid Based Image Result
![img10slide8](https://github.com/user-attachments/assets/c75eaae6-c36f-4fa5-a81e-58b985428630)
Sliding Window Denoising Result
![img10slide8x2](https://github.com/user-attachments/assets/ebe59e3d-1d90-4f12-ac4f-772d35986684)
Sliding Window Denoising X2 Result

- 

## References
1. [Intel Open Image Denoise](https://www.openimagedenoise.org/)
2. [NVIDIA Real-Time Noise Suppression](https://developer.nvidia.com/blog/nvidia-real-time-noise-suppression-deep-learning/)
3. Blender - A free and open-source 3D creation suite.
