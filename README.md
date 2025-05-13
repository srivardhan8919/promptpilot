# 🚀 PromptPilot — AI-Powered Prompt Enhancer

PromptPilot is a full-stack web application that intelligently analyzes, refines, and optimizes your AI prompts using the open-source Mistral-7B-Instruct model. By leveraging 4-bit quantization and a unique hybrid architecture—combining Google Colab hosting with your local React+Flask stack—PromptPilot delivers high-quality prompt improvements in real time.

---

## 🌟 Key Features

- **Prompt Improvement**  
  Automatically refines your raw prompts for clarity, creativity, and tone.

- **Memory-Efficient Inference**  
  4-bit NF4 quantization via BitsAndBytes lets a 7B-parameter model run in ~15 GB RAM.

- **Hybrid Hosting**  
  Model lives in Google Colab behind an ngrok tunnel; frontend/backend run locally.

- **Full-Stack Workflow**  
  React UI with authentication → Flask API → Colab-hosted LLM → back to UI.

- **Future-Ready**  
  MongoDB integration for user management and upcoming “prompt history” features.

---

## 📐 Architecture Overview

```text
┌────────────┐      ┌───────────────┐      ┌───────────────────────────┐
│ React Front │◀────│ Local Flask   │◀────│ Colab Notebook + ngrok    │
│ (Auth + UI) │      │ Backend + DB  │      │ • Quantized Mistral-7B    │
└────────────┘      └───────────────┘      └───────────────────────────┘
     ▲                   │   │                         ▲
     │                   └───┘                         │
     │           MongoDB (user creds + prompt history) │
     └─────────────────────────────────────────────────┘
````

> **Note:** The heavy LLM inference runs remotely in Colab due to its \~15 GB RAM demand. Local services handle UI, auth, and DB.

---

## ⚠️ Cautions & Requirements

* **RAM**: Minimum \~15 GB GPU RAM for the quantized model.
* **Latency**: ngrok tunneling may add 200–500 ms per request.
* **Security**: ngrok endpoints are public; avoid exposing sensitive data.
* **No Docker**: Deployment scripts (Docker/K8s) coming soon.

---

## 🛠️ Getting Started

### 1. Clone & Navigate

```bash
git clone https://github.com/srivardhan8919/promptpilot.git
cd promptpilot
```

### 2. Model Server (Colab)

1. Open `colab_model_server.ipynb` in Google Colab.
2. Run all cells to:

   * Install dependencies (transformers, bitsandbytes, flask, ngrok, etc.)
   * Authenticate with Hugging Face
   * Load and quantize Mistral-7B-Instruct
   * Start Flask + ngrok tunnel
3. Copy the generated `https://xxxx.ngrok.io` URL for your local config.

### 3. Backend (Local)

1. ```bash
   cd backend
   pip install -r requirements.txt
   ```
2. Create a `.env` file:

   ```ini
   MODEL_API_URL=https://xxxx.ngrok.io/generate
   MONGO_URI=mongodb://localhost:27017
   SECRET_KEY=your_jwt_secret
   ```
3. Run:

   ```bash
   python app.py
   ```

### 4. Frontend (Local)

1. ```bash
   cd frontend
   npm install
   ```
2. In `.env` or config:

   ```ini
   REACT_APP_API_URL=http://localhost:5001
   ```
3. Run:

   ```bash
   npm start
   ```

---

## 🔍 Usage

1. Sign up or log in on the React app.
2. Enter any prompt (e.g., “Draft a project update email”).
3. Receive one or more enhanced prompt versions instantly.

---

## 📦 Tech Stack

| Layer            | Technology                               |
| ---------------- | ---------------------------------------- |
| **Model**        | Mistral-7B-Instruct (4-bit NF4)          |
| **Inference**    | Hugging Face Transformers + BitsAndBytes |
| **Model Server** | Flask + ngrok (Google Colab)             |
| **API**          | Flask, Flask-CORS, JWT                   |
| **Frontend**     | React, Custom CSS                        |
| **Database**     | MongoDB                                  |

---

## 🔮 Roadmap

* **Prompt History & Analytics**
* **Multi-Model Support & Few-Shot Examples**
* **Prompt Scoring & Success Metrics**
* **Cloud Deployment** (AWS/GCP/Paperspace with GPU)
* **Docker & Kubernetes** automation

---

## 🤝 Contributing & Feedback

Found a bug or have an idea?

* Open an issue
* Submit a pull request
* Connect with me on [LinkedIn](https://www.linkedin.com/in/srivardhan-nutenki-207b55249/)

```
