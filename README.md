# NeoStore — Microservices E-Commerce Platform with ML Fraud Detection

A full-stack e-commerce platform built on a microservices architecture, integrated with a machine learning service that detects fraudulent product returns using **ResNet-50 (ImageNet pretrained)** with cosine similarity comparison between dispatch images and returned product images. Features Redis caching on hot API routes for near-real-time performance.

---

## ⚡ Performance Highlights

| Metric | Before | After |
|---|---|---|
| API Response Time | ~175 ms | **12 ms** |
| Fraudulent Returns (Validation Set) | Baseline | **Reduced by 95%** |

---

## 🏗️ Architecture Overview

```
┌─────────────┐     ┌─────────────────────────────────────┐
│   React.js  │────▶│           Node.js Backend            │
│  Frontend   │     │  (REST API · JWT Auth · Redis Cache) │
└─────────────┘     └──────────────┬──────────────────────┘
                                   │
               ┌───────────────────▼────────────────────┐
               │                                        │
        ┌──────▼──────┐                      ┌──────────▼──────────┐
        │   MongoDB   │                      │   Flask ML Service  │
        │   Database  │                      │   ResNet-50 +       │
        └─────────────┘                      │   Cosine Similarity │
                                             │   POST /upload      │
                                             └─────────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React.js |
| Backend | Node.js, Express |
| ML Service | Flask, ResNet-50 (ImageNet), cosine similarity |
| Database | MongoDB |
| Caching | Redis |
| Auth | JWT |

---

## ✨ Key Features

- **ML-powered fraud detection** — ResNet-50 (pretrained on ImageNet) extracts feature vectors from dispatch and return images; cosine similarity score above 0.8 marks the return as genuine, below as fraudulent. Achieves **95% fraud reduction** on the validation dataset
- **Redis caching** on hot API routes — slashed latency from 175ms to 12ms
- **Microservices architecture** — services are independently scalable and deployable
- **JWT authentication** with protected routes
- **Role-based flows** for customers and admins

---

## 🚀 Getting Started

### Prerequisites

- Node.js `16.x` or above
- MongoDB (local or Atlas)
- Redis server (`redis-server`)
- Python 3.8+ (for ML microservice)

### 1. Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file in `/backend`:

```
PORT=5000
DB_URL=<your_mongodb_connection_string>
SECRET_KEY=your_secret_key
```

Initialize the MongoDB database with the following collections:
`addressCollection`, `cartWishSave`, `orderCollection`, `products`, `productsSold`, `users`

Start the server:

```bash
node --watch server.js
```

### 2. Frontend Setup

Open `frontend/src/port.js` and update:

```js
export const BASE_URL = "http://localhost:<YOUR_PORT_NUMBER>";
```

Then:

```bash
cd frontend
npm install
npm run build
```

### 3. ML Microservice Setup

```bash
pip install flask flask-cors torch torchvision pillow scikit-learn
python new.py
```

> Accepts `POST /upload` with `file` (return image) and `dispatchImages[]` (original product images). Returns `{ result: "Genuine Product" | "Fraudulent Product", similarity: float }`

---

## 📁 Project Structure

```
NeoStore/
├── backend/          # Node.js REST API with Redis caching
├── frontend/         # React.js UI
├── demo images/      # Screenshots
└── new.py            # Flask ML microservice — ResNet-50 fraud detection (POST /upload)
```

---

## 📸 Demo

Screenshots available in the [`demo images/`](./demo%20images) folder.

---

## 👤 Author

**Ravikiran Pedapalli**  
[LinkedIn](https://linkedin.com/in/pedapalli-ravi-kiran) · [GitHub](https://github.com/ravikiranp04)
