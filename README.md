# 🛡️ Automated ViHSD Pipeline with Real-time Retraining
> **Developed by Vu Dai Duong - CE student at UIT**

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)

## Introduction
This project is an advanced content moderation system designed for **Vietnamese social media contexts**, combining **Rule-based filtering**, **Cross-lingual checks (Vietnamese & English)**, and **Deep Learning (Bi-LSTM)**.  
The system is built as an **Automated Pipeline** featuring an **Active Learning** mechanism. This allows the AI model to continuously evolve and improve based on user feedback. It also features a secure and interactive **Admin Dashboard** (incorporating UX enhancements) to streamline the data verification process.

## Project Structure
The system is designed to be self-sufficient. It will automatically generate configuration and model files if they are missing.

```text
ViHSD/
├── Embedding&Model/
│   ├── embedding/ 
│   │   └── cc.vi.300.vec              # [REQUIRED] Pre-trained FastText Vectors 
│   └── model/
│       ├── hate_speech_model.keras    # [Auto-gen] Trained AI Model
│       └── tokenizer.pickle           # [Auto-gen] Text Tokenizer
├── keyword/                           # [Auto-gen] All files below are created 
│   ├── keywords.json                  # if not present, containing default rules
│   ├── whitelist.json                 # and exception lists.
│   └── teencode.json                  
├── dataset/
│   ├── dataset.csv                    # [REQUIRED] Your training data
│   ├── feedback_pool.csv              # [Auto-gen] Stores user reports
│   └── approved_pool.csv              # [Auto-gen] Approved data for retraining
└── HateSpeech.ipynb                   # Main System Engine & UI
```
## Pre-trained Assets & Models (Required)
Due to file size limits, large pre-trained embeddings must be downloaded manually:
* **Word Embeddings:** `cc.vi.300.vec` (FastText Vietnamese - 300d, 2M vectors).
  * 👉 [**Download from Kaggle (Recommended)**](https://www.kaggle.com/datasets/aeryss/fasttext-vietnamese-word-vectors-full)
  * 👉 [**Alternative: Official FastText Source**](https://fasttext.cc/docs/en/crawl-vectors.html)

## Features
* **Hybrid & Cross-Lingual Detection:**
  * **Deep Learning:** Uses Bi-LSTM with FastText embeddings for semantic analysis of Vietnamese text.
  * **English Filter:** Integrated dictionary-based scanning to instantly flag English profanity.
  * **Teencode Support:** Optimized Regex engine to handle Vietnamese slang and internet jargon.
* **Contextual Intelligence:** Automatically handles "False Positives" using a dynamic **Whitelist** and exception rules, ensuring neutral words aren't flagged incorrectly.
* **Automated MLOps & Active Learning:**
  * **User Feedback Loop:** Users can report incorrect predictions directly via the Web UI.
  * **Smart Data Pipeline:** Validated data is automatically **mapped, deduplicated, and merged** into the main dataset.
  * **Real-time Retraining:** The system automatically triggers model fine-tuning and updates .keras files once the approved data threshold is reached.
* **Interactive Admin Dashboard:**
  * **Monkey Login UI:** A fun and functional authentication interface where the mascot reacts to password visibility (hides/shows eyes).
  * **Secure Moderation:** Tools for administrators to Review, Approve (Clean/Offensive/Hate), or Discard user reports.

## How to Run

### Run on Google Colab (Recommended)
You can run the entire project directly in your browser without local installation.

1.  **Open the notebook:** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/VuDaiDuong-325/ViHSD/blob/DesktopUIT/HateSpeech.ipynb)

2.  **[Requirement] Upload Data:** You only need to provide the **FastText vector** (cc.vi.300.vec) and your **dataset.csv**.

3.  **Configuration:**
    * Update *BASE_PATH* in Cell 2
    * Enter your [Ngrok Authtoken](https://dashboard.ngrok.com/get-started/your-authtoken) into the **Web App cell *(Cell 9)*** at:  
      *NGROK_TOKEN = "(PASTE_YOUR_TOKEN_HERE)"*.

5.  **Run All Cells:** Click **Runtime** > **Run all**.  
   *The system is designed to be self-generating. Upon the first execution, it will automatically create all necessary JSON configurations, directory structures, and train the initial model as long as the dataset and embedding vectors are provided.*
    * Access the Web Interface:
      * **User Interface**: Open the URL labeled **TRANG NGƯỜI DÙNG** in the cell output.
      * **Admin Dashboard**: Open the URL labeled **TRANG QUẢN TRỊ** in the cell output.

7.  **Testing & Moderation**
    * For **Users**:
      * **Check content:** 
        * Enter or paste a comment into the text box: *Nhập bình luận của bạn tại đây...*.
        * Click **KIỂM TRA NGAY** (Check) to view the classification result.
      * **Report Errors:** If the AI prediction is incorrect, click the **Báo cáo kết quả sai** (Report Error) button to submit the case.
    * For **Administrator**:
      * **Login:** Access the Admin URL and enter the password *(Default: admin123)*. You can also reach this page by clicking **Khu vực quản trị viên** (Admin Login) from the User Interface.
      * **Review Reports:** In the dashboard, you will see a list of user reports:
        * **Approve:** Click the correct label (*Clean*, *Offensive*, or *Hate*) in **Chọn nhãn chính xác** (Choose the correct label) column to confirm and move data to the training pool.
        * **Discard:** Click **Xóa rác** (Delete) to remove invalid or spam reports.
      * **Logout:** Click **Đăng xuất** (Logout) to secure your session.

## Technologies
* **Language:** Python
* **DL Framework:** TensorFlow / Keras (Bi-LSTM)
* **NLP Tools:** Regex, Emoji Library, FastText Embeddings
* **Web Framework:** Flask, PyNgrok (Tunneling)
