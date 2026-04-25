# 🛡️ ShieldMail

### Real-Time Spam & Phishing Detection System

ShieldMail is a cybersecurity-focused web application that detects spam messages and malicious (phishing) links in real time. It combines machine learning, URL analysis, and behavioral signals to help users stay protected from harmful email content.

---

## 🎯 Project Overview

ShieldMail was developed as part of a Web Software Development course project. The system analyzes incoming messages and provides:

* 📩 Spam classification
* 🔗 Malicious URL detection
* 🧠 Content and sentiment insights
* 🌍 Multilingual analysis

The goal is to simulate a **lightweight SOC-style email filtering system**, similar to real-world security tools.

---

## 👥 Team & Context

* **Institution**: ITMO University, St. Petersburg, Russia
* **Course**: Web Software Development
* **Lead Contributor**: Lamhamedi-Cherradi Younes
* **Project Type**: Academic Team Project

---

## 🚀 Features

### 🔍 Spam Detection

* Machine learning-based classification
* Detects common spam patterns and anomalies

### 🔗 Phishing & Malicious Link Detection

* Extracts URLs from email content
* Identifies suspicious or unsafe domains

### 💬 Sentiment & Content Analysis

* Detects urgency and manipulation language
* Helps identify social engineering attempts

### 🌐 Multilingual Support

* Supports multiple languages
* Useful for global phishing detection

### ⚡ Real-Time Processing

* Instant feedback using AJAX
* No page reload required

---

## 🏗️ System Architecture

```
Client (Browser)
       ↓
Frontend (HTML, JS, AJAX)
       ↓
Nginx (Reverse Proxy)
       ↓
Gunicorn (WSGI Server)
       ↓
Flask Backend (ML + Logic)
       ↓
MongoDB (Database)
```

---

## 🛠️ Technology Stack

| Layer       | Technology        | Purpose                     |
| ----------- | ----------------- | --------------------------- |
| Backend     | Python + Flask    | Core logic & ML integration |
| Frontend    | JavaScript + AJAX | Real-time interaction       |
| Database    | MongoDB           | Flexible data storage       |
| Web Server  | Nginx             | Reverse proxy & performance |
| WSGI Server | Gunicorn          | Production server           |

---

## ⚙️ Installation & Setup

### 1. Clone Repository

```bash
git clone https://github.com/yourusername/shieldmail.git
cd shieldmail
```

---

### 2. Create Virtual Environment

```bash
python3 -m venv venv
```

#### Activate Environment

* Linux / macOS:

```bash
source venv/bin/activate
```

* Windows:

```bash
venv\Scripts\activate
```

---

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

### 4. Start MongoDB

Make sure MongoDB is running locally:

```bash
mongod
```

---

### 5. Run the Application

```bash
python app.py
```

---

### 🌐 Access the App

Open your browser and go to:

```
http://localhost:5000
```

---

## 🚀 Production Deployment

### Run with Gunicorn

```bash
gunicorn -w 4 -b 0.0.0.0:8000 app:app
```

---

### Nginx Configuration Example

```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

---

## 🔐 Security Considerations

* ✅ Input sanitization to prevent injection attacks
* ✅ URL validation for phishing detection
* ✅ Reverse proxy protection via Nginx
* ✅ Basic traffic filtering and logging

---

## 📊 Future Improvements

* 🔍 Integration with threat intelligence APIs
* 🤖 Advanced ML models for higher accuracy
* 📈 Dashboard for analytics and logs (SIEM-style)
* 🔐 User authentication system
* ☁️ Cloud deployment (AWS / Docker)

---

## 📄 License

This project is for academic and educational purposes.

---

## 🤝 Contributing

Contributions are welcome! Feel free to fork the repository and submit a pull request.

---

## ⭐ Acknowledgments

* Open-source community
* Cybersecurity research resources
* Academic mentors and instructors

---
