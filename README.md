# Land Use Land Cover Segmentation Using Sentinel-1A SAR Data

This repository contains the source code for my undergraduate thesis titled  
**"Land Use Land Cover Segmentation using Synthetic Aperture Radar Data on Dhaka Division, Bangladesh"**. 
Published: Sadia Khan, et al. "Land use land cover segmentation using synthetic aperture radar data on Dhaka division, Bangladesh", Proc. SPIE 13734, Eighth International Conference on Machine Vision and Applications (ICMVA 2025), 1373407 (1 Aug 2025); https://doi.org/10.1117/12.3079561
The project leverages **Sentinel-1A Synthetic Aperture Radar (SAR)** imagery to segment land cover types in the Dhaka region using deep learning models like **U-Net** and **DeepLabV3+**.
The full publication can be found here: https://www.spiedigitallibrary.org/conference-proceedings-of-spie/13734/1373407/Land-use-land-cover-segmentation-using-synthetic-aperture-radar-data/10.1117/12.3079561.full 
---

## Project Motivation

In Bangladesh, rice is the staple food and a key contributor to the national economy. However, the monsoon season overlaps with major rice cultivation periods, creating cloud cover that hampers optical satellite imaging.  
To overcome this, **SAR imagery** is used since it can **penetrate clouds** and operate in **all weather conditions**, enabling year-round monitoring of agricultural land.

---

## Objectives

- Use **Sentinel-1A SAR data** to segment land into meaningful classes (e.g., water, forest, farmland)
- Compare segmentation performance with benchmark studies using Sentinel-2A (optical imagery)
- Prove SAR’s viability for **monsoon-season crop monitoring** in tropical climates

---

## Methodology Overview

The end-to-end workflow followed in this project:

1. **Download Sentinel-1A SAR imagery** from the Copernicus Open Access Hub  
2. **Preprocess SAR data** using tools like **QGIS** and **SNAP**  
   (band extraction, cropping, VV/VH stacking)  
3. **Generate 512×512 patches** from SAR images and annotated Bing masks  
4. **One-hot encode** annotated masks for use in deep learning models  
5. **Train U-Net and DeepLabV3+ models** using TensorFlow/Keras  
6. **Evaluate performance** using **Accuracy**, **IoU**, **F1 Score**, and visual inspection

---

## Models Used

- **U-Net**: A CNN-based architecture widely used for biomedical and satellite image segmentation.
- **DeepLabV3+** with **MobileNetV2** backbone: Used for lightweight, high-resolution semantic segmentation.

---

## File Overview

### `sar_patches_maker.py`
- Preprocesses SAR + annotated Bing images into 512×512 patches using the `patchify` library
- Saves patch datasets for model training

### `sar-lulc-code.py`
- Trains a **U-Net** model using TensorFlow/Keras
- Applies class reweighting and a combination of **Dice Loss** and **Focal Loss**
- Outputs segmentation results and evaluation metrics

---

## Classes

The annotated dataset includes five land cover classes:

| Class             | Color  | Index |
|------------------|--------|-------|
| Farmland         | Black  | 0     |
| Water            | Blue   | 1     |
| Forest           | Aqua   | 2     |
| Urban Built-up   | Red    | 3     |
| Meadow           | Yellow | 4     |

---

## Evaluation Metrics

- **Accuracy**
- **Intersection over Union (IoU)**
- **F1 Score**
- **Training vs Validation Loss Curves**
- **Visual comparison** of predictions and masks

---

## Requirements

Install packages via pip:

```bash
pip install tensorflow==2.2.1
pip install keras==2.5
pip install segmentation-models
pip install patchify
```

If using Google Colab, some of these may already be available.

---

## Study Area

- **Location:** Dhaka Division, Bangladesh  
- **SAR Data:** Sentinel-1A (VV and VH bands, GRD product)  
- **Ground Truth:** Annotated high-resolution Bing imagery

---

## Key Results

| Model         | Mean Accuracy | Mean IoU | Mean F1 Score |
|---------------|---------------|----------|----------------|
| U-Net         | 75.88%        | 0.27     | 0.40           |
| DeepLabV3+    | 82.00%        | 0.25     | 0.36           |

---

## Author

**Sadia Khan**  
Undergraduate Thesis, Department of Computer Science & Engineering  
Independent University, Bangladesh

---

## 📜 License

This project is released for **academic and research use**.  
If you use this work or any part of the code, please cite or acknowledge the author.
