# Comparative Evaluation of CNNs and Vision Transformers for Skin Lesion Classification

### MAAI901 – Deep Learning for Visual Data
University of Wollongong in Dubai  
Group Project

## Project Overview

This project compares different deep learning models for classifying skin lesion images. We wanted to investigate how convolutional neural networks (CNNs) perform compared to Vision Transformers, and whether models pretrained on general images or dermatology-specific data give better results.

We also looked at how full fine-tuning compares with linear probing, where the pretrained backbone is kept frozen. Another important part of our work was checking for duplicate images between datasets, as these can affect the reliability of evaluation results.

Finally, we tested the models on a separate dataset to see how well they generalise to images outside the training data and whether performance varies across different skin tones.

## Datasets Used

We used three datasets:

**ISIC 2019:** Contains dermoscopic images covering eight skin lesion classes.

**PAD-UFES-20:** Contains clinical skin lesion images captured using smartphones. Its labels were mapped to the corresponding ISIC classes.

**DDI (Diverse Dermatology Images):** Used only for external evaluation, including comparisons across Fitzpatrick skin-tone groups.

After preprocessing and removing records with conflicting exact-duplicate labels, the combined development dataset contained 27,601 images:

| Split | Number of Images |
|---|---:|
| Training | 19,341 |
| Validation | 4,131 |
| Testing | 4,129 |

The eight classification categories are MEL, NV, BCC, AK, BKL, DF, VASC and SCC.

The datasets are not included in this repository.

## Models Compared

We evaluated seven pretrained models:

**CNNs**
- ResNet-50
- DenseNet-121
- MobileNetV2
- MobileNetV3-Large

**Vision Transformers**
- ViT-B/16
- CLIP ViT-B/16
- DermLIP ViT-B/16

Each model was tested using linear probing and full fine-tuning, giving a total of 14 experiments.

## Project Implementation

The project was implemented in Python using Google Colab, with libraries including PyTorch, torchvision, timm and OpenCLIP.

The work was divided into two main notebooks.

### 1. Dataset Preprocessing

The first notebook prepares the datasets for training. It includes image validation, label mapping, exact and near-duplicate checks, geometric verification and group-aware train/validation/test splitting.

The preprocessing process was designed to reduce data leakage between splits. We also documented the remaining limitations of near-duplicate detection.

### 2. Model Training and Evaluation

The second notebook trains and evaluates the seven models using the prepared datasets.

The main evaluation metric was macro-F1 because the dataset contains an uneven number of images across classes.

Other metrics included accuracy, balanced accuracy, melanoma recall, ROC-AUC and confusion matrices. We also used group bootstrapping and statistical comparisons to assess the reliability of the results.

The trained models were evaluated on the held-out development test set and on DDI for external generalisation.

## Main Results

Full fine-tuning performed better than linear probing across all seven models.

DermLIP ViT-B/16 achieved the highest development test macro-F1 score of 0.708, followed by CLIP at 0.684 and ViT-B/16 at 0.675.

However, performance dropped considerably during external evaluation on DDI, where the binary malignancy AUC ranged from approximately 0.55 to 0.65.

This showed that strong performance on the development datasets does not necessarily mean a model will perform equally well on a different clinical dataset.

The skin-tone analysis did not identify a statistically significant performance difference, although the available data was too limited to rule out important differences.

## How to Use the Notebooks

The notebooks were developed in Google Colab.

1. Download or open the preprocessing notebook in Colab.
2. Obtain the required datasets separately and configure the Google Drive paths.
3. Run preprocessing to prepare the dataset and generate the split files.
4. Open the training and evaluation notebook.
5. Configure the paths to the preprocessed data and required pretrained weights.
6. Run the relevant training or evaluation cells.

The notebooks depend on external datasets and Google Drive files, so some paths will need to be updated before running them in a different environment.

The full experiments may require substantial GPU resources.

## Limitations

The experiments used a single training seed and a fixed training budget. Some linear probes may not have fully converged.

Although duplicate checks and group-aware splitting were used, not all possible near-duplicates could be ruled out.

The external DDI dataset also differs from the training data in image characteristics and diagnostic coverage, which limits direct comparisons.

This project is intended for academic research and evaluation only. It should not be used for clinical diagnosis.

## Project Demo

A separate phone-based demonstration is available here:

https://alialjawi.github.io/skin-lesion-phone-demo/

Demo source code:

https://github.com/AliAljawi/skin-lesion-phone-demo

## Group Members

Kainaz Chohan - 8273273
Bushra Siddiqui - 8044764
Meyyappan Venkatesh - 1644750
Ali Aljawi - 1641487
Arbab - 

## Acknowledgements

We used publicly available research datasets, pretrained models and open-source Python libraries for this project. The original dataset creators and model authors are acknowledged in the project report.
