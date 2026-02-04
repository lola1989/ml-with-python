# Chest X-ray Disease Classification

A deep learning project to detect 14 thoracic pathologies from chest X-ray images using transfer learning with DenseNet121.

## Project Overview

This project develops a multi-label classification model to identify 14 different thoracic pathologies from X-ray images. The model uses a subset of the NIH ChestX-ray8 dataset and implements transfer learning with DenseNet121, a convolutional neural network pretrained on ImageNet.

**Research Question:** Can a deep learning model accurately detect and classify 14 thoracic pathologies from chest X-ray images?

## Dataset

**NIH ChestX-ray8 Dataset**
- 5,000 frontal-view chest X-ray images
- 14 disease labels: Atelectasis, Cardiomegaly, Consolidation, Edema, Effusion, Emphysema, Fibrosis, Hernia, Infiltration, Mass, Nodule, Pleural Thickening, Pneumonia, Pneumothorax
- Severe class imbalance (some diseases <1% prevalence)

**Source:** [National Institutes of Health](https://nihcc.app.box.com/v/ChestXray-NIHCC)

**Note:** Labels were extracted from radiological reports using Natural Language Processing and were not manually verified.

## Methodology

### 1. Data Preprocessing
- Multi-label stratified train/validation/test split (70/15/15)
- Image resizing to 224×224 pixels
- Normalization using dataset-specific mean and standard deviation
- Data augmentation (random flips, rotations, affine transforms)

### 2. Model Architecture
- **Base Model:** DenseNet121 pretrained on ImageNet
- **Modification:** Replaced final classifier layer with 14-output layer
- **Loss Function:** Weighted Binary Cross-Entropy (to handle class imbalance)
- **Optimizer:** Adam (learning rate = 0.0001)
- **Training:** Early stopping with patience of 15 epochs

### 3. Evaluation Metrics
- **AUC-ROC:** Measures discrimination ability across all thresholds
- **Average Precision (AP):** Particularly important for imbalanced classes
- **F1-Score:** Balance between precision and recall

### 4. Model Interpretation
- GradCAM visualization to understand which regions the model focuses on
- Helps identify if the model is learning relevant anatomical features

## Results

The model performance is evaluated using:
- Per-disease AUC-ROC, Average Precision, and F1-scores
- ROC curves for all 14 pathologies
- GradCAM heatmaps showing model attention regions

Results are saved in `results/final_metrics.json`

## References

Wang, X., Peng, Y., Lu, L., Lu, Z., Bagheri, M., & Summers, R. M. (2017). ChestX-Ray8: Hospital-Scale Chest X-Ray Database and Benchmarks on Weakly-Supervised Classification and Localization of Common Thorax Diseases. IEEE CVPR. [DOI: 10.1109/CVPR.2017.369](http://dx.doi.org/10.1109/CVPR.2017.369)

## License

This project is for educational purposes. The NIH ChestX-ray8 dataset has its own license terms that must be followed.

## Disclaimer

This model is for research and educational purposes only. It is not intended for clinical diagnosis or treatment decisions. Always consult qualified healthcare professionals for medical advice.
