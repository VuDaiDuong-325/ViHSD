# 🛡️ Vietnamese Hate Speech Detection System

## 📝 Introduction
This project is a hybrid content moderation system designed to detect hate speech and offensive language on Vietnamese social media. It combines **Rule-based filtering** (handling teencode, slang, and mixed variations) with a **Deep Learning model (Bi-LSTM)** trained on embedded word vectors. The system features a real-time web interface powered by Flask and Ngrok for instant text classification.

## 📥 Pre-trained Assets & Models (Required)
Due to GitHub's file size limits, large pre-trained embedding vectors and model weights are hosted externally. **You must download these files to run the project:**

* **Word Embeddings:** `cc.vi.300.vec` (FastText Vietnamese)
* **Trained Models:** `hate_speech_model.h5` & `tokenizer.pickle` 
* 👉 [**Click here to download from Google Drive**](https://drive.google.com/drive/folders/1m41I9HwABPZX5RsOGwcBbmECC7rEnOEe?usp=sharing)

*Please place these files inside the `embedding/` and `model/` folders respectively after downloading.*

## ✨ Features
* **Hybrid Approach:** Prioritizes whitelist/blacklist keywords before using AI inference.
* **Teencode Processing:** Automatically translates Vietnamese internet slang into standard text.
* **Bi-LSTM Model:** Captures contextual semantic meanings effectively.
* **Web App Demo:** Interactive UI to test comments in real-time.

## 🚀 How to Run

### Method 1: Run on Google Colab (Recommended)
You can run the entire project directly in your browser without local installation.

1.  **Open the notebook:** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/VuDaiDuong-325/ViHSD/blob/DesktopUIT/HateSpeech.ipynb)

2.  **Upload Data:**
    * Upload `teencode.json` and your dataset files to the Colab environment (or mount Google Drive as instructed in the notebook).
    * Ensure `cc.vi.300.vec` is placed in the correct path.

3.  **Setup Ngrok:**
    * Sign up for a free account at [dashboard.ngrok.com](https://dashboard.ngrok.com/get-started/your-authtoken).
    * Copy your **Authtoken** and paste it into the "Web App" cell.

4.  **Run All Cells:** * Click **Runtime** > **Run all**.
    * Click the public URL (e.g., `xxxx.ngrok-free.app`) generated in the output to access the interface.

## 🛠 Technologies
* **Language:** Python
* **DL Framework:** TensorFlow / Keras
* **NLP Tools:** NLTK, Regex, FastText
* **Web Framework:** Flask, PyNgrok

---
*Developed by **Vu Dai Duong***
