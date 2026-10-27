# Brain Tumor Segmentation from MRI Images

## Overview

This project focuses on the automatic segmentation of brain tumor regions from Magnetic Resonance Imaging (MRI) scans using deep learning. A U-Net-based convolutional neural network is developed to identify tumor regions at the pixel level and generate segmentation masks.

The project explores medical image preprocessing, data augmentation, model training, and segmentation performance evaluation.

## Objectives

- Develop a U-Net-based model for brain tumor segmentation.
- Preprocess MRI images and their corresponding segmentation masks.
- Improve generalization using data augmentation.
- Evaluate segmentation performance using standard metrics.
- Compare predicted masks with ground-truth masks.

## Dataset

The project uses the publicly available [Brain Tumor Dataset — Segmentation and Classification](https://www.kaggle.com/datasets/indk214/brain-tumor-dataset-segmentation-and-classification) from Kaggle.

The segmentation dataset contains MRI images and their corresponding tumor masks for three tumor types:

| Tumor Type | Number of Images |
|---|---:|
| Glioma | 1,108 |
| Meningioma | 1,416 |
| Pituitary Tumor | 1,860 |
| **Total** | **4,384** |

The dataset was divided into training (70%), validation (15%), and test (15%) subsets.

**Note:** The dataset is not included in this repository. Download it from Kaggle and prepare the image and mask folders before running the notebook.

## Methodology

### 1. Data Preprocessing

- Resized images to `256 × 256` pixels.
- Converted images into tensors and normalized pixel values to the `[-1, 1]` range.
- Applied binary thresholding to segmentation masks.
- Matched MRI images with their corresponding ground-truth masks.

### 2. Data Augmentation

The following transformations were applied to improve model generalization and reduce overfitting:

- Horizontal and vertical flipping
- Small-angle rotations
- Brightness and contrast adjustments
- Mild noise addition

### 3. Model Architecture

The project uses a **U-Net architecture**, widely used for biomedical image segmentation.

The model consists of:

- **Encoder:** Extracts image features through successive downsampling stages.
- **Bottleneck:** Learns deeper, more complex image representations.
- **Decoder:** Reconstructs spatial resolution to generate pixel-level segmentation predictions.
- **Skip connections:** Combine encoder features with decoder features to preserve spatial details.

The encoder uses progressively increasing channel sizes of 64, 128, 256, and 512, followed by a bottleneck with 1,024 channels.

### 4. Training Configuration

- **Framework:** PyTorch
- **Optimizer:** Adam
- **Learning rate:** 0.001
- **Loss function:** Combined Dice Loss and Binary Cross-Entropy (DiceBCELoss)
- **Learning rate scheduler:** ReduceLROnPlateau

### 5. Post-processing

The model's pixel-wise probability predictions are converted into binary segmentation masks using a threshold. Small isolated regions are removed, and the largest connected component is retained to obtain cleaner predictions.

## Results

The model achieved the following reported segmentation metrics:

| Metric | Score |
|---|---:|
| Dice Score | **0.8047** |
| Intersection over Union (IoU) | **0.6475** |
| Sensitivity | **0.7876** |
| Specificity | **0.9971** |

The results indicate that the model can identify tumor regions while maintaining high specificity. Some segmentation errors remain, particularly around small tumors and unclear tumor boundaries.

## Technologies Used

- Python
- PyTorch
- Deep Learning
- Convolutional Neural Networks (CNNs)
- U-Net
- Medical Image Processing
- Image Segmentation
- Data Augmentation
- NumPy
- Jupyter Notebook

## Project Structure

```text
Brain_Tumor_Seg/
├── main.ipynb
├── .gitignore
└── datas/                 # Local dataset; not tracked by Git
```

## How to Run

1. Clone the repository:

   ```bash
   git clone https://github.com/tugcepekoz/Brain_Tumor_Seg.git
   cd Brain_Tumor_Seg
   ```

2. Download the dataset from [Kaggle](https://www.kaggle.com/datasets/indk214/brain-tumor-datasetsegmentation-and-classification).

3. Prepare the MRI images and corresponding masks according to the directory paths expected by `main.ipynb`.

4. Install the required Python packages used in the notebook.

5. Open and run `main.ipynb` in Jupyter Notebook or JupyterLab.

*Note: Exact dataset directory paths and package versions should be checked in the notebook before running the project.*

## Future Improvements

- Experiment with alternative segmentation architectures.
- Improve segmentation of small tumors and uncertain boundaries.
- Evaluate performance separately for each tumor type.
- Explore additional loss functions and hyperparameter optimization.
- Investigate more efficient training strategies.

## References

- Ronneberger, O., Fischer, P., & Brox, T. (2015). *U-Net: Convolutional Networks for Biomedical Image Segmentation.*
- [PyTorch Documentation](https://pytorch.org/docs/stable/index.html)

---

**Author:** Tuğçe Peköz
