# 🌸 Iris Flower Classification

[![Python](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Flask-API-green.svg)](https://flask.palletsprojects.com/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-Model-orange.svg)](https://scikit-learn.org/)
[![Docker](https://img.shields.io/badge/Docker-Containerized-blue.svg)](https://www.docker.com/)

A streamlined MLOps pipeline that trains a Random Forest model using `scikit-learn`, wraps it in a Flask web API, and containerizes the entire environment with Docker. The frontend features a modern **glassmorphism** UI built from scratch using pure Vanilla CSS.

---

## ✨ Features

- **Premium UI:** A sleek, fully responsive glassmorphism interface with micro-animations and loading states.
- **Machine Learning Pipeline:** Automatically trains a Random Forest Classifier on the famous Iris Dataset.
- **RESTful API:** Exposes endpoints to classify new flower measurements via JSON payloads.
- **Containerized:** Fully Dockerized for seamless deployment to cloud providers (e.g., Render, Heroku).

---

## 📂 Project Structure

```text
Iris-Flower-Classifier/
├── static/             # Static assets (images, CSS if extracted)
├── templates/
│   └── index.html      # Premium Glassmorphism UI
├── app.py              # Flask API server & inference endpoints
├── train.py            # Model training script
├── iris_model.pkl      # Serialized random forest model (generated after training)
├── Dockerfile          # Container environment configuration
├── requirements.txt    # Application dependencies
└── .gitignore          # Version control file exclusions
```

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed:
- [Python 3.12+](https://www.python.org/downloads/)
- [Docker](https://www.docker.com/get-started) (optional, for containerization)

### 1. Environment Configuration

It is recommended to use an isolated environment like `venv` or Conda.

**Using venv:**
```bash
python -m venv venv
# On Windows PowerShell
.\venv\Scripts\Activate.ps1
# On macOS/Linux Bash
source venv/bin/activate
```

**Using Conda:**
```bash
conda create -n iris-mlops python=3.12 -y
conda activate iris-mlops
```

### 2. Dependency Installation

Install the necessary project dependencies:

```bash
pip install -r requirements.txt
```

---

## ⚙️ Execution Guide

### 1. Train the Model

Before running the server, you **must** train the model. This script generates the `iris_model.pkl` file used by the Flask app.

```bash
python train.py
```
*Expected Output:*
```text
Training the model...
Model saved successfully!
```

### 2. Run the Web App Locally

Start the Flask server:

```bash
# On Windows PowerShell
$env:PORT=5001; python app.py

# On macOS/Linux Bash
PORT=5001 python app.py
```

Open `http://127.0.0.1:5001` or `http://localhost:5001` in your web browser to interact with the new interface!

---

## 🐳 Running with Docker

You can easily run this application in a self-contained Docker environment. The `Dockerfile` is already configured to train the model during the image build process and use `gunicorn` for the web server.

### 1. Build the Docker Image
```bash
docker build -t iris-api .
```

### 2. Start the Container
```bash
docker run -e PORT=5001 -p 5001:5001 iris-api
```

---

## ☁️ Deployment (Render)

This project is optimized for deployment on [Render](https://render.com/) using Docker.

1. Create a new **Web Service** on Render.
2. Connect your GitHub repository.
3. Choose **Docker** as the environment.
4. Render will automatically detect the `Dockerfile` and build the image.
5. The `Dockerfile` exposes port `10000` and binds to the `$PORT` environment variable provided by Render.

---

## 📖 API Documentation

### Health Check / UI Route
- **Endpoint:** `GET /`
- **Description:** Renders the frontend UI form dashboard.

### Prediction Route
- **Endpoint:** `POST /predict`
- **Headers:** `Content-Type: application/json`
- **Description:** Accepts JSON input with Iris flower features and returns the predicted class.
- **Payload Format:**
  ```json
  {
    "sepal_length": 5.1,
    "sepal_width": 3.5,
    "petal_length": 1.4,
    "petal_width": 0.2
  }
  ```
- **Success Response (200 OK):**
  ```json
  {
    "class": "Setosa"
  }
  ```
- **Error Response (400 Bad Request):**
  ```json
  {
    "error": "Invalid request payload: <error_message>"
  }
  ```
