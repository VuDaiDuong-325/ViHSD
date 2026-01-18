# 🛡️ Vietnamese Hate Speech Detection System

## Introduction
This project is a hybrid content moderation system designed to detect hate speech and offensive language on Vietnamese social media. It combines **Rule-based filtering** (handling teencode, slang, and mixed variations) with a **Deep Learning model (Bi-LSTM)** trained on embedded word vectors. The system features a real-time web interface powered by Flask and Ngrok for instant text classification.

## 📥 Pre-trained Assets & Models (Required)
Due to GitHub's file size limits, the large pre-trained embedding vectors and model weights are hosted externally. **You must download these files to run the project locally or on Colab:**

* **Word Embeddings:** `cc.vi.300.vec` (FastText Vietnamese)
* **Trained Models:** `hate_speech_model.h5` & `tokenizer.pickle` 
* 👉 [**Click here to download from Google Drive**](https://drive.google.com/drive/folders/1m41I9HwABPZX5RsOGwcBbmECC7rEnOEe?usp=sharing)

*Please place these files inside the `embedding/` and `model/` folders respectively after downloading.*

## Features
* **Hybrid Approach:** Prioritizes whitelist/blacklist keywords before using AI inference.
* **Teencode Processing:** automatically translates Vietnamese internet slang into standard text.
* **Bi-LSTM Model:** Captures contextual semantic meanings effectively.
* **Web App Demo:** Interactive UI to test comments in real-time.

## How to Run

### Method 1: Run on Google Colab (Recommended)
You can run the entire project directly in your browser without installation.

1.  Open the notebook:  
    [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](LINK_TO_YOUR_COLAB_FILE)  
    *(Note: Replace `LINK_TO_YOUR_COLAB_FILE` with your actual GitHub file link after uploading)*

2.  **Upload Data:**
    * Upload `teencode.json` and your dataset files to the Colab environment (or mount Google Drive as instructed in the notebook).

3.  **Setup Ngrok:**
    * Sign up for a free account at [dashboard.ngrok.com](https://dashboard.ngrok.com/get-started/your-authtoken).
    * Copy your **Authtoken**.
    * In the "Web App" cell, replace `"PASTE_YOUR_TOKEN_HERE"` with your actual token.

4.  **Run All Cells:** * Click **Runtime** > **Run all**.
    * Click the public URL generated at the last cell to access the Web Interface.

## Technologies
* **Language:** Python
* **DL Framework:** TensorFlow / Keras
* **NLP:** NLTK, Regex
* **Web Framework:** Flask, PyNgrok

