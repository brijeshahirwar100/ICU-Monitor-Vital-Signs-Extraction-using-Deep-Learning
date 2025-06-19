# ICU Monitor Vital Signs Extraction using Deep Learning

![ICU Monitor](https://your-image-link-if-needed) <!-- optional: insert an image or demo gif -->

## 📌 Project Overview

This project presents a deep learning-based pipeline to **automatically extract vital signs** — such as **Heart Rate (HR)**, **Blood Pressure (BP)**, and **Oxygen Saturation (SpO₂)** — from ICU monitor images. The system combines **EfficientNet** for monitor detection and **PaddleOCR** for text recognition, enabling near real-time, accurate, and automated ICU data interpretation.

---

## ⚙️ Architecture

### 🔹 1. Monitor Segmentation  
- **Model**: EfficientNet-B4  
- **Purpose**: Detect and localize ICU monitor screens from full-scene images  
- **Accuracy**: IOU score of **94–96%**  
- **Preprocessing**: Padding, skew correction, resizing, and cropping to improve accuracy

### 🔹 2. Text Detection & Mapping  
- **Tool**: PaddleOCR  
- **Logic**: Geometric layout analysis and keyword-based nearest-number association  
- **Accuracy**: 88–92% OCR accuracy on real ICU images  

---

## 🧠 Vital Sign Detection Logic

- **Heart Rate (HR)**: Detected via "HR" keyword or green text mask if keyword fails  
- **SpO₂ & RR**: Identified through positional and keyword proximity logic  
- **Blood Pressure (SBP/DBP) & MAP**: Handled via `/` separation, bounding boxes, and keyword mapping  
- **ECG Detection**: Green contour isolation; fallback to `neurokit2` simulation if undetected

---

## 🧪 Dataset & Training

- **Type**: Mixed dataset (real ICU scenes + synthetic augmentations)  
- **Augmentations**: Brightness, skew, rotation, Gaussian noise  
- **Environment**: Google Colab + Local RTX 3060 GPU  
- **Optimizer**: Adam, LR = 0.001, 50 epochs  

---

## 📈 Results

| Metric                  | Value        |
|------------------------|--------------|
| Segmentation IOU       | 94–96%       |
| OCR Text Accuracy      | 88–92%       |
| End-to-End Accuracy    | ~85%         |
| Execution Speed        | ~1 sec/frame |

---

## 🔍 Observations

- **HR**: Typically green; appears in top 30% of screen  
- **SpO₂ & RR**: Inconsistent colors; detected with keywords + position heuristics  
- **BP**: SBP/DBP often separated by `/`; MAP often in brackets or nearby  
- **Challenges**: Lighting variance, layout inconsistency, text overlap, OCR misreads  

---

## 🚀 Future Enhancements

- Real-time video stream support  
- ECG waveform interpretation for arrhythmia detection  
- Multilingual OCR support  
- Integration with hospital IT systems for live alerts  

---

## 👨‍💻 Authors

- Brijesh Ahirwar  
- Dhanush Kamatam  
- Kushaan Mahajan  
- Gowtham Palli  
- **Supervisor**: Dr. Amritanshu Pandey, Department of Electronics Engineering, IIT (BHU)

---

## 📄 Citation

If you use this work, please consider citing or referencing our exploratory project under EC291, IIT (BHU) Varanasi.

---

## 🗂️ Files Included

- `model/` – Trained model checkpoints  
- `src/` – Code for segmentation, OCR, and logic pipeline  
- `notebooks/` – Jupyter notebooks for testing  
- `samples/` – Example ICU monitor images  
- `results/` – Output examples with vital signs  
- `README.md` – Project overview

---

## 🔗 Resources

- [EfficientNet](https://arxiv.org/abs/1905.11946)  
- [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)  
- [Neurokit2](https://neurokit2.readthedocs.io/en/latest/)

