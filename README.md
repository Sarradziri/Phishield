# 🛡️ Phishing Email Detector

Detect phishing emails with machine learning, through two interfaces:

- **Chrome extension**: analyzes the email you are reading directly in your webmail.
- **Web interface**: paste or type an email and get an instant verdict.

🎥 **Demo video:** https://drive.google.com/file/d/1bpFnErSccBoj_08CMHwNpRNi3QhDJoZO/view?usp=sharing

---

## ✨ Features

- Classifies an email as **phishing** or **legitimate**
- Chrome extension with popup, and visual alert/safe icons
- React web app for manual email analysis
- Several ML models trained and compared (Logistic Regression, Naive Bayes, Decision Tree, Random Forest, SGD, XGBoost, MLP) <!-- TODO: confirm which one is used in production -->
- Text vectorization + label encoding saved as `.pkl` files for fast inference
- Dockerized backend for the extension

## 🗂️ Project Structure

```
.
├── GoogleExtension/        # Chrome extension + its Python API
│   ├── manifest.json       # Extension config
│   ├── background.js       # Service worker
│   ├── content.js          # Reads email content from the page
│   ├── popup/              # Popup UI (html/css/js)
│   ├── icons/              # Extension icons
│   ├── models/             # Trained models, vectorizers, encoder (.pkl)
│   ├── app.py              # Backend API
│   ├── model.py, check.py  # Model loading and prediction logic
│   ├── requirements.txt
│   └── Dockerfile
└── Web interface/
    ├── frontend/           # React app (EmailAnalyser component)
    ├── server/             # Python backend (mainFask.py, model.py)
    └── *.pkl               # Trained models and vectorizers
```

## 🧰 Tech Stack

| Part | Technologies |
|------|--------------|
| ML | Python, scikit-learn, XGBoost <!-- TODO: confirm --> |
| Backend | Flask <!-- TODO: confirm --> |
| Web frontend | React, CSS |
| Extension | JavaScript, Chrome Extension (Manifest V3?) <!-- TODO --> |
| DevOps | Docker |

## 🧠 How It Works

1. The email text is extracted (by the extension's content script or typed into the web app).
2. It is sent to the backend API.
3. The text is vectorized with the saved vectorizer, then passed to the trained model.
4. The prediction (phishing / legitimate) is returned and displayed to the user.

**Dataset:** <!-- TODO: name, size, source -->
**Results:** <!-- TODO: accuracy / precision / recall / F1 per model -->

## 🚀 Getting Started

### Prerequisites
- Python 3.12+
- Node.js 18+ and npm
- Google Chrome
- Docker (optional)

### 1. Chrome extension backend

```bash
cd GoogleExtension
pip install -r requirements.txt
python app.py
```

Or with Docker:

```bash
docker build -t phishing-extension .
docker run -p 5000:5000 phishing-extension   # TODO: confirm port
```

### 2. Load the extension in Chrome

1. Open `chrome://extensions`
2. Enable **Developer mode**
3. Click **Load unpacked** and select the `GoogleExtension` folder
4. Open an email in your webmail and click the extension icon

### 3. Web interface

```bash
# Backend
cd "Web interface/server"
python mainFask.py

# Frontend (new terminal)
cd "Web interface/frontend"
npm install
npm start
```

The app runs on `http://localhost:3000`.

## 📸 Screenshots

<!-- TODO: add 2-3 screenshots (extension popup, web app, safe vs phishing result) -->

## 🔮 Future Improvements

- Analyze links and attachments, not only text
- Multilingual support (French / Arabic)
- Deploy the backend online
- Retrain periodically on new phishing samples

## 👩‍💻 Author

**Sarra** <!-- TODO: add GitHub / LinkedIn links -->
