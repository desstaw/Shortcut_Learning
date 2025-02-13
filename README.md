# Mitigating Shortcut Learning in Machine Learning Models

### Overview
This repository explores **shortcut learning**, a phenomenon where machine learning models rely on spurious correlations instead of genuine class-relevant features. We conduct experiments on two distinct datasets:

- **International Skin Imaging Collaboration (ISIC) dataset** – A real-world medical image classification dataset. The presence of unintended visual artifacts (e.g., medical patches) introduces biases that influence model predictions.

- **Colored MNIST (CMNIST) dataset** – A variant of MNIST with controlled biases, designed for systematic evaluation of shortcut learning. We classify digits **"0"** and **"2"**, which share structural similarities while remaining distinguishable.

#### Dataset Variants:
- **Colored Background** – Digit **"0"** has a red background.
- **Colored Digits** – Digits are directly colored red.
- **Dynamic Left Patch** – A red patch is placed on the left side of digit **"0"**.

---

### Model Architecture
We adapt **AlexNet**, a deep convolutional network originally designed for ImageNet, for binary classification.

#### Modifications:
1. **Feature Extraction Layers** – Frozen to retain pre-trained ImageNet features.
2. **Fully Connected Layers** – Modified for two-class classification.
3. **Activation Extraction** – Activations are taken from the **FC2** layer for further analysis.

---

### Mitigating Shortcut Learning
We introduce two key strategies to mitigate shortcut learning:

#### 1. Sparse Autoencoder (SAE)
A **Sparse Autoencoder (SAE)** is employed to transform feature activations into a structured latent space, reducing shortcut dependencies.

**How it works:**
- **Encoder** – Compresses activations while enforcing sparsity.
- **Decoder** – Reconstructs activations while suppressing shortcut-related neurons.
- **Sparsity Constraints** – L1 regularization is applied to limit neuron activations.

#### 2. Correlation-Based Neuron Suppression
This technique identifies and suppresses shortcut-sensitive neurons using **Pearson correlation analysis**.

**Steps:**
- **Pearson Correlation Analysis** – Identifies neurons highly correlated with artifacts.
- **Neuron Muting** – Suppresses neurons influenced by shortcuts.
- **Final Reconstruction** – Retains core discriminative features while reducing shortcut learning.

---

### Usage
#### Data Preparation
Prepare the patches for the MNIST dataset:
```bash
Data_preparation/MNIST_28_patch_preparation.ipynb
```

#### Training AlexNet on ISIC or CMNIST Datasets
```bash
ERM/MNIST_28_alexnet_eval.ipynb
ERM/ISIC_228_alexnet_eval.ipynb
```

#### Running Feature Extraction, Correlation Analysis, Sparse Projections, and Muting
```bash
Sparse_muting/MNIST_foreground_SAE_muting.ipynb
Sparse_muting/MNIST_background_SAE_muting.ipynb
Sparse_muting/MNIST_dyn_lp_SAE_muting.ipynb
Sparse_muting/ISIC_SAE_muting.ipynb
```

---

### Citation
If you find this work useful, please consider citing our repository.

---

