# 🛡️ Automated ViHSD Pipeline with Real-time Retraining
> **Developed by Vu Dai Duong - CE student at UIT**

## Introduction
This project is an advanced content moderation system for Vietnamese, combining **Rule-based filtering** and **Deep Learning (Bi-LSTM)**. The system is built as an **Automated Pipeline** featuring an **Active Learning** mechanism that allows the model to continuously evolve and improve from user feedback through a secure Admin Dashboard.

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
* **Hybrid Detection:** Uses optimized Regex for teencode/slang and Bi-LSTM for deep semantic context.
* **Contextual Intelligence:** Automatically handles "False Positives" using a built-in **Whitelist**.
* **Active Learning Loop:**
  * **User Feedback:** Real-time reporting via Web UI.
  * **Admin Dashboard:** Secure review and approval system.
  * **Real-time Retraining:** Automatically triggers model fine-tuning and updates .keras files after reaching a **100-approved-entry** threshold

## How to Run

### Run on Google Colab (Recommended)
You can run the entire project directly in your browser without local installation.

1.  **Open the notebook:** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/VuDaiDuong-325/ViHSD/blob/DesktopUIT/HateSpeech.ipynb)

2.  **[Requirement] Upload Data:** You only need to provide the **FastText vector** (cc.vi.300.vec) and your **dataset.csv**.

3.  **Configuration:**
    * Update *BASE_PATH* in Cell 2
    * Enter your [Ngrok Authtoken](https://dashboard.ngrok.com/get-started/your-authtoken) into the **Web App cell *(Cell 9)*** at:
      *NGROK_TOKEN = "(PASTE_YOUR_TOKEN_HERE)"*.

5.  **Run All Cells:** Click **Runtime** > **Run all**. The system is designed to be self-generating. Upon the first execution, it will automatically create all necessary JSON configurations, directory structures, and train the initial model as long as the dataset and embedding vectors are provided.
    * Access the Web Interface:
      * **User Interface**: Open the URL labeled **TRANG NGƯỜI DÙNG** in the cell output.
      * **Admin Dashboard**: Open the URL labeled **TRANG QUẢN TRỊ** in the cell output.

6.  **Testing & Moderation**
    * For **Users**:
      * **Check content:** 
        * Enter or paste a comment into the text box: *Nhập bình luận của bạn vào đây...*.
        * Click **KIỂM TRA NGAY** (Check) to view the classification result.
      * **Report Errors:** If the AI prediction is incorrect, click the **Báo cáo sai** (Report Error) button to submit the case.
    * For **Administrator**:
      * **Login:** Access the Admin URL and enter the password *(Default: admin123)*. You can also reach this page by clicking **Admin Login** from the User Interface.
      * **Review Reports:** In the dashboard, you will see a list of user reports:
        * **Approve:** Click the correct label (*Clean*, *Offensive*, or *Hate*) to confirm and move data to the training pool.
        * **Discard:** Click **Xóa bỏ (Rác/Spam)** (Delete) to remove invalid or spam reports.
      * **Logout:** Click **Đăng xuất** (Logout) to secure your session.

## Technologies
* **Language:** Python
* **DL Framework:** TensorFlow / Keras (Bi-LSTM)
* **NLP Tools:** Regex, Emoji Library, FastText Embeddings
* **Web Framework:** Flask, PyNgrok (Tunneling)
