# 🤟 Sign Language Translator

A computer vision project that recognizes American Sign Language (ASL) alphabet gestures from images and converts them into text and speech.  
The model is served through a web app with real-time webcam input, deployed with Docker.


## 📌 Overview

Communication between sign language users and non-signers remains a major challenge.

This project builds an end-to-end **ASL alphabet translator**: a fine-tuned MobileNetV2 model classifies hand gestures, and a Flask web app captures webcam frames, detects the hand with MediaPipe, and returns the predicted letter as text and audio.


## 🎯 Objectives

- Classify ASL alphabet gestures from hand images  
- Improve accuracy through transfer learning and fine-tuning  
- Build a web interface that translates webcam input into text and speech  
- Package the full application for reproducible deployment with Docker  


## 🧠 Key Features

- **Transfer learning** with MobileNetV2, fine-tuning the last 50 layers  
- **MediaPipe hand detection** to crop the region of interest before prediction  
- **Web app** with live webcam input (Flask backend, HTML/JS frontend)  
- **Text-to-speech** output using Google Text-to-Speech (gTTS)  
- **Docker** containerization for deployment  


## 🗂️ Dataset

- ASL alphabet hand gesture images  
- Labeled by letter class, organized in folders and loaded with Keras `ImageDataGenerator`  
- Split into training and validation sets  


## ⚙️ Methodology

1. Data preprocessing  
   - Pixel normalization  
   - Binarization  
   - Folder-based label assignment with `ImageDataGenerator`  

2. Model Development  
   - **Initial approach:** MobileNetV2 as a frozen feature extractor + fully connected dense layers  
   - **Final approach:** unfroze the last 50 layers of MobileNetV2 and fine-tuned on the ASL dataset  
   - Also experimented with EfficientNetB4 and ResNet  

3. Training  
   - **Initial:** Adam optimizer, 15 epochs  
   - **Final:** up to 50 epochs with early stopping, `ReduceLROnPlateau`, and regularization  

4. Inference Pipeline (Web App)  
   - MediaPipe detects the hand and crops the region of interest  
   - Resize to 224×224, convert to grayscale, normalize  
   - Model predicts the letter → displayed as text and played as audio  


## 📊 Model Evaluation

- Training and validation accuracy and loss tracked per epoch  
- Initial and final approaches compared on validation accuracy  


## 🛠️ Tech Stack

- Python  
- TensorFlow / Keras (MobileNetV2)  
- MediaPipe  
- Flask  
- HTML / JavaScript (webcam capture, AJAX)  
- gTTS (Google Text-to-Speech)  
- Docker  


## 📁 Project Structure

```
Sign-Language-Translator/
│
├── notebooks/           # Data preparation & model training
├── app/                 # Flask backend & inference pipeline
├── static/              # Frontend (HTML, JS)
├── models/              # Trained model
├── Dockerfile
└── README.md
```


## 🚀 Results

| Approach | Train Accuracy | Validation Accuracy |
|---|---|---|
| Initial (frozen MobileNetV2, 15 epochs) | 63.1% | 60.4% |
| **Final (fine-tuned last 50 layers, early stopping)** | **83.2%** | **84.1%** |

- Fine-tuning improved validation accuracy by **+23.7 pts** (60.4% → 84.1%)  
- Built a working web app that turns webcam gestures into text and speech  
- Deployed the full stack with Docker  


## 📌 Limitations

- Static alphabet letters only; words, sentences, and motion-based signs are not supported  
- Evaluated on a validation split only, without a separate test set  
- Real-time lag from webcam capture, hand cropping, and prediction  
- Docker image compatibility issues between ARM64 and AMD64 architectures  


## 🔧 Future Work

- Evaluate on a held-out test set and with real webcam images  
- Extend to word- and sentence-level translation using sequence models (LSTM, Transformers)  
- Reduce inference latency for smoother real-time use  
- Build multi-architecture Docker images  


## 👤 Author

Park, Eunsoo  
Dhakal, Sarthak  
Tsegaselassie, Wengel A  

**My role:** Data Preprocessing, Model fine-tuning


## ✔️ Summary

> An end-to-end ASL alphabet translator that fine-tunes MobileNetV2 (validation accuracy 60.4% → 84.1%) and serves predictions as text and speech through a Dockerized Flask web app
