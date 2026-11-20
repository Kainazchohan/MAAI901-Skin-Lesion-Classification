
# Skin Lesion Classification Using CNNs and Vision Transformers

## Project Overview

This project was developed for MAAI901 – Deep Learning for Visual Data at the University of Wollongong in Dubai.

We compared seven pretrained deep learning models for classifying skin lesions into eight categories. The aim was to see how CNNs and Vision Transformers perform using the same training setup, and whether their performance changes when tested on a different dataset.

We also looked at the effects of fine-tuning, duplicate images, class imbalance and differences in performance across skin tones.

This project is for academic research only and is not intended for clinical diagnosis.

## Datasets Used

We used three datasets:

- **ISIC 2019:** Dermoscopic images used for training, validation and testing.
- **PAD-UFES-20:** Smartphone clinical images combined with ISIC 2019 for model development.
- **DDI:** Used separately for external evaluation and skin-tone analysis.

The datasets are not included in this repository and must be downloaded separately.

Dataset links:

- ISIC 2019: https://challenge.isic-archive.com/data/
- PAD-UFES-20: https://data.mendeley.com/datasets/zr7vgbcyr2/1
- DDI: https://ddi-dataset.github.io/

After cleaning and checking for conflicting duplicate labels, the combined development dataset contained 27,601 images.

## Models Used

We compared seven pretrained models:

1. ResNet-50
2. DenseNet-121
3. MobileNetV2
4. MobileNetV3-Large
5. ViT-B/16
6. CLIP ViT-B/16
7. DermLIP ViT-B/16

Each model was tested using two training approaches:

- **Linear probing:** Keeping the pretrained backbone frozen and training only the classification layer.
- **Full fine-tuning:** Updating all model weights during training.

This gave us 14 experiments in total.

## Data Preprocessing

Before training, we checked the images for duplicates and conflicting labels. We also used group-aware dataset splitting to reduce the possibility of related images appearing across training, validation and test sets.

The final dataset was divided into:

- Training: 19,341 images
- Validation: 4,131 images
- Testing: 4,129 images

Images were resized, and data augmentation was applied during training. Class-weighted loss was used to help address class imbalance.

## Training and Evaluation

The experiments were carried out in Google Colab using PyTorch.

We evaluated the models using accuracy, macro-F1, precision, recall, confusion matrices and ROC-AUC. Macro-F1 was the main evaluation metric because some skin lesion classes had fewer images than others.

We also compared melanoma detection at fixed specificity levels and tested the fine-tuned models on DDI to evaluate performance on independent images and across Fitzpatrick skin-tone groups.

## Main Results

Fine-tuned DermLIP achieved the highest development test macro-F1 score of 0.708. CLIP and ViT-B/16 also performed well compared with the CNN models.

However, performance dropped considerably on the external DDI dataset, where binary malignancy AUC scores ranged from approximately 0.55 to 0.65.

These results showed that good performance on the development dataset does not necessarily mean a model will perform equally well on new clinical images.

## Installing Dependencies

The notebooks were developed and run in Google Colab.

To install the required Python libraries in another environment, use:

```bash
pip install -r requirements.txt
```

The dependency versions are not pinned because the original Colab library versions were not recorded.

DermLIP pretrained weights are loaded from Hugging Face:

`redlessone/DermLIP_ViT-B-16`

The notebooks use Google Drive for accessing data and saving results, so paths and storage settings may need to be adjusted outside Colab.

## Project Demo

A separate phone-based demonstration is available here:

https://alialjawi.github.io/skin-lesion-phone-demo/

Demo source code:

https://github.com/AliAljawi/skin-lesion-phone-demo

## Group Members

Ali Aljawi - 1641487  
Bushra Siddiqui - 8044764  
Kainaz Chohan - 8273273  
Meyyappan Venkatesh - 1644750  
Mohammed Khan - 1657331  

## Acknowledgements

We used publicly available research datasets, pretrained models and open-source Python libraries for this project. The original dataset creators and model authors are acknowledged in our project report.
