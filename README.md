Shortcut Learning in Machine Learning Models

Overview

This repository investigates shortcut learning, a phenomenon where machine learning models rely on spurious correlations rather than learning genuine class-relevant features. The study employs two distinct datasets:

International Skin Imaging Collaboration (ISIC) dataset for real-world medical image classification.

Colored MNIST (CMNIST) dataset with controlled biases for systematic evaluation.

By analyzing these datasets, we explore how models develop unintended dependencies and propose mitigation strategies using Sparse Autoencoders and Correlation-Based Neuron Suppression.

Datasets

1. ISIC Dataset

The International Skin Imaging Collaboration (ISIC) dataset is widely used for skin lesion classification. However, unintended visual artifacts (e.g., medical patches) create biases, influencing model predictions.

Dataset Structure:

Class

Description

Benign-NoPatch

Benign skin lesion without artifacts

Benign-Patch

Benign skin lesion with artifacts

Malignant-NoPatch

Malignant skin lesion without artifacts

Malignant-Patch

Malignant skin lesion with artificially introduced artifacts



2. Colored MNIST (CMNIST) Dataset

A variant of MNIST, the CMNIST dataset introduces artificial biases to test shortcut learning. We classify digits "0" and "2", as they share similar structures but remain distinguishable.

Dataset Variants:

Colored Background: Digit "0" has a red background.

Colored Digits: Digits are directly colored red.

Dynamic Left Patch: A red patch is placed on the left side of digit "0".



Model Architecture

We use AlexNet, a deep convolutional network originally designed for ImageNet, and adapt it for binary classification.

1. AlexNet Modifications

Feature Extraction Layers: Frozen to retain pre-trained ImageNet features.

Fully Connected Layers: Modified for two-class classification.

Activation Extraction: Activations are taken from the FC2 layer for further analysis.

📷 Modified AlexNet Structure:

Mitigating Shortcut Learning

1. Sparse Autoencoder (SAE)

We employ a Sparse Autoencoder to transform feature activations into a structured latent space that removes shortcut dependencies.

How it works:

Encoder: Compresses activations, enforcing sparsity.

Decoder: Reconstructs activations, suppressing shortcut-related neurons.

Sparsity Constraints: L1 regularization applied to limit neuron activations.


2. Correlation-Based Neuron Suppression

Pearson Correlation Analysis: Identifies neurons highly correlated with artifacts.

Neuron Muting: Suppresses shortcut-sensitive neurons.

Final Reconstruction: Retains core discriminative features while reducing shortcut learning.

