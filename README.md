# 🛡️ Vietnamese Hate Speech Detection System
> Developed by Vu Dai Duong - CE student at UIT

## Introduction
This project is a hybrid content moderation system designed to detect hate speech and offensive language on Vietnamese social media. It combines **Rule-based filtering** (handling teencode, slang, and mixed variations) with a **Deep Learning model (Bi-LSTM)** trained on embedded word vectors. The system features a real-time web interface powered by Flask and Ngrok for instant text classification.

## 📂 Project Structure
Below is the mandatory directory structure for the project to function correctly:

```text
ViHSD/
├── Config/
│   └── ngrok_token.txt            # Store your Ngrok Authtoken (Local only)
├── Embedding&Model/
│   ├── embedding/
│   │   └── cc.vi.300.vec          # FastText Vietnamese Vectors
│   └── model/
│       ├── hate_speech_model.keras # Bi-LSTM Trained model
│       └── tokenizer.pickle       # Saved tokenizer
├── keyword/
│   ├── keywords.json              # Blacklist/Rule-based categories
│   ├── teencode.json              # Vietnamese slang dictionary
│   └── whitelist.json             # Exception/Safe word list
├── dataset/
│   └── (Your training CSV files)
└── HateSpeech.ipynb               # Main Notebook (Colab)
```
**[WARNING]**
**Important Note**: If you do **NOT** organize your files according to the hierarchy above, you **MUST** manually update the file paths (links) in **Cell 2** (Config cell) of the notebook to match your custom setup.

## Pre-trained Assets & Models (Required)
Due to GitHub's file size limits, large pre-trained embedding vectors and model weights are hosted externally. **You must download these files to run the project:**

* **Word Embeddings:** `cc.vi.300.vec` (FastText Vietnamese)
* **Trained Models:** `hate_speech_model.keras` & `tokenizer.pickle` 
* 👉 [**Click here to download from Google Drive**](https://drive.google.com/drive/folders/1m41I9HwABPZX5RsOGwcBbmECC7rEnOEe?usp=sharing)

## Features
* **Hybrid Approach:** Prioritizes whitelist/blacklist keywords before using AI inference.
* **Smart Preprocessing:**
* * Automatically handles **Emoji Unicode** and **Emoticons**.
  * Converts icons into **Vietnamese semantic text** to improve model accuracy.
  * Translates **Teencode** and **internet slang** into standard Vietnamese.
* **Bi-LSTM Model:** Captures contextual semantic meanings effectively.
* **Web App Demo:** Interactive UI to test comments in real-time.

## How to Run

### Run on Google Colab (Recommended)
You can run the entire project directly in your browser without local installation.

1.  **Open the notebook:** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/VuDaiDuong-325/ViHSD/blob/DesktopUIT/HateSpeech.ipynb)

2.  **Upload Data:**
    * Upload all folders & files to the Colab environment (or mount Google Drive as instructed in the notebook).

3.  **Setup Ngrok:**
    * Sign up for a free account at [dashboard.ngrok.com](https://dashboard.ngrok.com/get-started/your-authtoken).
    * Copy your **Authtoken** and paste it into the **Web App cell** at:
      *NGROK_TOKEN = "(PASTE_YOUR_TOKEN_HERE)"*

4.  **Run All Cells:** Click **Runtime** > **Run all**.
    * Click the public URL (e.g., `xxxx.ngrok-free.app`) generated in the output to access the interface.

5.  **Test:**
    * Write or paste a comment into the box: *Nhập bình luận của bạn vào đây...*.
    * Click **KIỂM TRA NGAY** to see the classification result.

## Technologies
* **Language:** Python
* **DL Framework:** TensorFlow / Keras (Bi-LSTM)
* **NLP Tools:** Regex, Emoji Library, FastText Embeddings
* **Web Framework:** Flask, PyNgrok (Tunneling)
