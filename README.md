# CIFAR-10 Image Classification API (FastAPI + Render)

## Overview

This repository contains the **backend inference API** for a CIFAR-10 image classification project. The model is built using **MobileNetV2 (Transfer Learning)** and deployed as a **FastAPI service on Render**.

The API accepts an image file, preprocesses it correctly, performs inference, and returns the predicted class with confidence.

---

## Model Details

* **Architecture:** MobileNetV2 (Transfer Learning)
* **Task:** CIFAR-10 Image Classification
* **Input Size:** `96 × 96 × 3`
* **Preprocessing:** `tf.keras.applications.mobilenet_v2.preprocess_input`
* **Output:** Predicted class label + confidence score

---

## Tech Stack

* Python
* TensorFlow / Keras
* FastAPI
* Uvicorn
* Pillow
* NumPy
* Render (Cloud Deployment)

---

## API Endpoints

### Health Check

```http
GET /
```

**Response**

```json
{
  "status": "API running"
}
```

---

### Prediction Endpoint

```http
POST /predict
```

**Request**

* Form-data
* Key: `file`
* Value: Image file (`.jpg`, `.jpeg`, `.png`)

**Response**

```json
{
  "predicted_class": "cat",
  "confidence": 0.87
}
```

---

## Live Deployment

* **Base URL:** [https://cifar10-fastapi-deploy-1.onrender.com](https://cifar10-fastapi-deploy-1.onrender.com)
* **Swagger Docs:** [https://cifar10-fastapi-deploy-1.onrender.com/docs](https://cifar10-fastapi-deploy-1.onrender.com/docs)

---

## Preprocessing Pipeline (Critical)

All preprocessing is handled **only on the backend**:

1. Convert image to RGB
2. Resize to `96 × 96`
3. Convert to NumPy array
4. Apply `preprocess_input`
5. Expand batch dimension

This ensures consistency between training and inference.

---

## Frontend UI

The user-facing interface is built using **Streamlit** and deployed separately.

* **Streamlit App:** [https://cifar10-app-ui-645uclhwrasvjwwswszule.streamlit.app/](https://cifar10-app-ui-645uclhwrasvjwwswszule.streamlit.app/)

---

## How to Run Locally

```bash
pip install -r requirements.txt
uvicorn main:app --reload
```

Then open:

```
http://127.0.0.1:8000/docs
```

---

## Notes

* This service is deployed on Render Free Tier
* The service may sleep after inactivity
* First request after sleep may take a few seconds

---

## Author

Rishav Nagpal
