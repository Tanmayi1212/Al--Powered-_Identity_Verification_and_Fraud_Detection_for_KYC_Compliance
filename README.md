# 🔐 AI-Powered Identity Verification & Fraud Detection Ecosystem

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-Async-green.svg)](https://fastapi.tiangolo.com/)
[![PyTorch](https://img.shields.io/badge/PyTorch-DeepLearning-red.svg)](https://pytorch.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-NoSQL-darkgreen.svg)](https://www.mongodb.com/)

> **"Identity is the new perimeter."**
> This project is an enterprise-grade KYC (Know Your Customer) solution that merges Deep Learning, Graph Theory, and modern Web APIs to provide a proactive defense against financial identity fraud.

---

## 🚀 Why This Project is Unique

Unlike traditional KYC systems that merely digitize documents, this ecosystem acts as a **Proactive Fraud Prevention Engine**. It is designed with "Banking-Level" intelligence, moving beyond text extraction into **behavioral and structural integrity analysis**.

* **Multi-Layered AI Defense**: Combines CNNs for pixel-level tampering detection and GNNs for identifying organized fraud rings.
* **Privacy by Design**: Automated data masking and PII protection compliant with global standards.
* **Enterprise Ready**: Features audit trails, bulk processing, and automated compliance reporting.

---

## 📸 Project Showreel (Visual Proof)

### 1. User Onboarding & Real-Time Extraction

*Description: Shows the asynchronous upload process and the immediate "Smart Preview" with masked data.*

> <img width="1365" height="595" alt="Screenshot 2026-04-02 120615" src="https://github.com/user-attachments/assets/9990df06-4171-4a73-8674-e74b4bd48a74" />


---

### 2. Admin Fraud Dashboard

*Description: High-level analytics showing risk scores, daily fraud trends, and flagged documents.*

><img width="1365" height="603" alt="Screenshot 2026-04-02 120430" src="https://github.com/user-attachments/assets/9f3d3eb4-1dd3-4413-8081-79f6bfca0061" />
<img width="1351" height="594" alt="Screenshot 2026-04-02 120444" src="https://github.com/user-attachments/assets/7b1b7c11-4f88-4654-84ac-ff65632bdf94" />
<img width="1334" height="599" alt="Screenshot 2026-04-02 120501" src="https://github.com/user-attachments/assets/1c1a73d0-bba6-480b-a69a-7ed478e373fa" />
<img width="1340" height="597" alt="Screenshot 2026-04-02 120512" src="https://github.com/user-attachments/assets/547f9cb5-0f49-4cca-9637-5f1a83ffdab0" />
<img width="1346" height="593" alt="Screenshot 2026-04-02 120523" src="https://github.com/user-attachments/assets/8fe747a7-bb5b-4f27-aa95-74105213bb7f" />
<img width="1350" height="600" alt="Screenshot 2026-04-02 120541" src="https://github.com/user-attachments/assets/48fcdefa-2506-4f04-885b-7a6109d6fbe4" />




---

## ✨ Core Features

### 🛡️ 1. Intelligent Fraud Engine

* **CNN-Based Tampering Detection**
  Detects Moire patterns (screen-spoofing) and font inconsistencies to identify manipulated documents.

* **GNN-Based Network Analysis**
  Identifies fraud rings by detecting hidden links between accounts (shared phone numbers, duplicate IDs).

* **Duplicate Detection**
  Prevents identity replay attacks by cross-checking submissions against historical data.

---

### 📄 2. Advanced Document Processing

* **Real-Time Smart Preview**
  Instant extraction of Name, DOB, and ID fields to reduce manual corrections.

* **Image Quality Guard**
  Rejects blurry, cropped, or low-resolution uploads before processing.

* **Multi-Document Support**
  Automatically detects PAN and Aadhaar cards in a unified flow.

---

### ⚖️ 3. Compliance & Enterprise Tools

* **Automated Data Masking**
  Masks sensitive fields (e.g., `XXXX-XXXX-1234`).

* **Audit-Ready PDF Reports**
  Generates compliance-ready reports with fraud scores and timestamps.

* **Bulk Verification**
  Supports CSV/Excel uploads for enterprise-scale operations.

---

## 🏗 System Architecture

```
┌─────────────┐      ┌──────────────────────────────┐      ┌──────────────┐
│  Client App ├─────►│  FastAPI (Async Middleware)  ├─────►│  EasyOCR/CNN │
└─────────────┘      └──────────────┬───────────────┘      └──────┬───────┘
                                   │                             │
                                   ▼                             ▼
                    ┌──────────────────────────────┐      ┌──────────────┐
                    │  GNN Fraud Network Analyzer  │◄────►│   MongoDB    │
                    └──────────────────────────────┘      └──────────────┘
```

---

## 🛠 Tech Stack

| Component             | Technology                         |
| --------------------- | ---------------------------------- |
| **Backend Framework** | FastAPI (Async & High Performance) |
| **Deep Learning**     | PyTorch (CNN), EasyOCR             |
| **Database**          | MongoDB (NoSQL)                    |
| **Image Processing**  | OpenCV, Pillow                     |
| **Data Extraction**   | Regex & Spatial Parsing            |

---

## ⚙️ Quick Start (Developer Setup)

### 1. Prerequisites

* Python 3.8+
* MongoDB instance
* Tesseract OCR (optional hybrid extraction)

---

### 2. Installation & Run

```bash
# Clone repository
git clone <repo-url>
cd AI-KYC-Fraud-Ecosystem

# Install dependencies
pip install -r requirements.txt

# Configure environment
echo "MONGO_URI=mongodb://localhost:27017" > .env
echo "DB_NAME=kyc_database" >> .env

# Run server
uvicorn app.main:app --reload
```

---

## 📡 API Interface (Glimpse)

### POST `/verify-kyc`

**Response:**

```json
{
  "status": "Success",
  "docType": "PAN",
  "fraudScore": 12,
  "riskLevel": "Low",
  "parsed": {
    "name": "TANMAYI NADIPALLI",
    "idNumber": "XXXXX1234X",
    "isMasked": true
  },
  "flags": []
}
```

---

## 🗺 Roadmap

* [ ] **Phase 1**: Face Matching (ID vs Selfie)
* [ ] **Phase 2**: Liveness Detection (Video-based)
* [ ] **Phase 3**: Blockchain Audit Trails

---

## 🤝 Contributing

Contributions are welcome. Open an issue before major changes.

---

## 📄 License

Licensed under the MIT License.

---

**⭐ Star this repo if you find it useful for your Fintech/AI journey!**
