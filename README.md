# Star Tracker Centroid Estimation Using Deep Learning

## Overview

This project explores a deep-learning approach to star centroid estimation in images acquired by a Star Tracker, a sensor used for spacecraft attitude determination.

Developed in MATLAB, the project combines image preprocessing, Gaussian target-mask generation and a Convolutional Neural Network (CNN) to estimate star locations in input images.

## Methodology

The implementation is organized into two main stages.

### 1. Data Preparation — data_star

The first script processes the input star images and generates the dataset used by the neural network.

The processing pipeline includes:
- Loading JPEG (.jpg) images from a user-specified directory.
- Resizing images to 128 × 128 pixels.
- Applying Gaussian filtering to reduce image noise.
- Detecting bright regions through intensity thresholding.
- Extracting star centroid coordinates using MATLAB's regionprops function.
- Generating Gaussian target masks centered at the detected star positions.

The preprocessed images and corresponding masks are stored in a MATLAB structure and saved to data.mat.

### 2. CNN Training and Evaluation — convolutional

The second script loads data.mat, prepares the input images and target masks, and trains a CNN.

The dataset is randomly shuffled and split into three subsets:

| Dataset | Proportion |
|---|---:|
| Training | 70% |
| Validation | 20% |
| Test | 10% |

The CNN consists of convolutional layers, ReLU activations, max-pooling, batch normalization and transposed convolutional layers.

The network is trained using:
- **Optimizer:** Adam
- **Loss function:** Mean Squared Error (MSE)
- **Maximum epochs:** 50
- **Mini-batch size:** 64
- **Initial learning rate:** 0.0003

After training, predictions are generated for the test set and evaluated using Mean Squared Error (MSE) and Root Mean Squared Error (RMSE).

## Repository Structure

```text
StarTracker/
├── README.md
├── docs/
│   └── Star_tracker.pdf
└── src/
    ├── data_star
    └── convolutional
```

The MATLAB scripts are stored in src/. The project report is available in docs/Star_tracker.pdf.

## Requirements

- MATLAB
- Deep Learning Toolbox
- Image Processing Toolbox

## Getting Started

### 1. Prepare the input images

Place the star images in a local directory. The data_star script currently expects JPEG (.jpg) files.

Before running the script, update the folder_path variable to point to the directory containing the images. The script currently sets the number of images to 1000, so this value should be consistent with the files available in that directory.

### 2. Generate the dataset

Run data_star from MATLAB.

The script preprocesses the images, generates the corresponding Gaussian target masks and saves the resulting dataset as data.mat.

### 3. Train and evaluate the CNN

Make sure data.mat is available in the MATLAB current working directory, then run convolutional.

The script loads the generated dataset, performs the training/validation/test split, trains the CNN and evaluates its predictions on the test set.

## Documentation

The project report is available at [docs/Star_tracker.pdf](docs/Star_tracker.pdf).

## Academic Project

This project investigates the application of deep learning and image processing techniques to star centroid estimation, a key step in vision-based spacecraft attitude determination.