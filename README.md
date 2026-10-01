<div align="center">

# Plant Disease Detection

### Snap a leaf, name the disease, get a treatment — a Streamlit app over a MobileNetV2 classifier

![Python](https://img.shields.io/badge/python-3.x-3776AB?logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-app-FF4B4B?logo=streamlit&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-Keras-FF6F00?logo=tensorflow&logoColor=white)
![Models](https://img.shields.io/badge/models-MobileNetV2%20·%20ResNet50%20·%20VGG16-6f42c1)
![Dataset](https://img.shields.io/badge/data-PlantVillage-2ea44f)
![Status](https://img.shields.io/badge/status-research%20project-lightgrey)
![License](https://img.shields.io/badge/license-MIT-blue)

[What it does](#what-it-does) ·
[The models](#the-models) ·
[Run it](#run-it) ·
[Paper](#research-paper)

</div>

---

A farmer photographs a sick tomato leaf; seconds later the app names the
disease, recommends a pesticide, and maps the nearest plant doctor, pesticide
store and nursery. The classifier behind it is a **MobileNetV2** fine-tuned on
the [PlantVillage](https://www.kaggle.com/datasets/abdallahalidev/plantvillage-dataset)
leaf dataset, with ResNet50 and VGG16 trained alongside it for comparison.

<p align="center">
<img src="Readme/Screenshot%202024-08-12%20085225.png" width="80%" alt="Plant Disease Detection home page">
</p>

## What it does

| Step | What happens |
| :--- | :--- |
| **1. Capture** | Upload a leaf photo or snap one with the webcam |
| **2. Diagnose** | The image is resized to 256×256, preprocessed, and classified in a few seconds |
| **3. Recommend** | The predicted disease is matched to a pesticide from [`pesticide.xlsx`](pesticide.xlsx) |
| **4. Locate** | A Folium map shows nearby plant doctors, pesticide stores and nurseries |

<p align="center">
<img src="Readme/Screenshot%202024-08-12%20090532.png" width="46%" alt="Uploading a leaf image">
<img src="Readme/Screenshot%202024-08-12%20091010.png" width="46%" alt="Prediction and pesticide recommendation">
</p>
<p align="center">
<img src="Readme/Screenshot%202024-08-12%20090640.png" width="80%" alt="Map of nearby plant doctors">
</p>

## The models

Three architectures were trained and compared across epoch budgets
(100 / 200 / 500 / 1000), with accuracy and loss curves saved per run:

| Model | Role | Where |
| :--- | :--- | :--- |
| **MobileNetV2** | Lightweight model served by the app | [`train_function.py`](train_function.py), [`plant_disease_detection.py`](plant_disease_detection.py) |
| **ResNet50** | Deeper comparison (PyTorch + TensorFlow) | [`Resnet/`](Resnet/) |
| **VGG16** | Baseline comparison, per-epoch plots | [`vgg16/`](vgg16/) |

Training curves live in [`vgg16/`](vgg16/) (`accuracy_comparison.png`,
`loss_comparison.png`) and the per-run logs/CSVs beside them.

## Run it

```bash
git clone https://github.com/harshakalluri1403/Plant-Disease-Detection.git
cd Plant-Disease-Detection

pip install streamlit tensorflow opencv-python pillow pandas numpy folium streamlit-folium openpyxl

streamlit run plant_disease_detection.py
```

Then open http://localhost:8501.

> **Before running:** `plant_disease_detection.py` loads the trained model from a
> hard-coded path (`model_file = '.../model_6.h5'`). Point it at your own trained
> `.h5` model — train one with [`train_function.py`](train_function.py) on the
> PlantVillage dataset, or drop in an existing checkpoint.

## Research paper

This work was written up as a paper in collaboration with **IIIT Kurnool** —
[Plantdisease.pdf](Plantdisease.pdf).

## Tech stack

Streamlit · TensorFlow / Keras · MobileNetV2 · ResNet50 · VGG16 · OpenCV ·
Folium · pandas

## License

Released under the [MIT License](LICENSE).
