# 🔐 AI-Powered Identity Verification & Fraud Detection for KYC Compliance

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104%2B-009688.svg)](https://fastapi.tiangolo.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Latest-green.svg)](https://www.mongodb.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A production-ready FastAPI service that performs automated KYC (Know Your Customer) document verification using OCR technology. The service extracts and validates information from Indian identity documents (PAN Card, Aadhaar Card) with intelligent field parsing and fraud detection capabilities.

---

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [System Architecture](#-system-architecture)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [API Documentation](#-api-documentation)
- [Database Schema](#-database-schema)
- [Testing](#-testing)
- [Troubleshooting](#-troubleshooting)
- [Roadmap](#-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

- **📄 Multi-Document Support**: Automatic detection and processing of PAN and Aadhaar cards
- **🔍 OCR Processing**: Powered by Tesseract OCR for accurate text extraction
- **🧠 Intelligent Parsing**: Regex-based field extraction for PAN number, Aadhaar number, name, DOB, etc.
- **💾 MongoDB Integration**: Persistent storage of processed documents and extracted data
- **⚡ Fast Processing**: Asynchronous endpoints with performance metrics
- **📊 Structured Output**: Clean JSON responses with parsed fields
- **🔒 Input Validation**: File type and size validation
- **📈 Processing Metrics**: Track processing time for each document

---

## 🛠 Tech Stack

| Component             | Technology                  |
| --------------------- | --------------------------- |
| **Backend Framework** | FastAPI                     |
| **OCR Engine**        | Tesseract OCR (pytesseract) |
| **Database**          | MongoDB                     |
| **Image Processing**  | Pillow (PIL)                |
| **Language**          | Python 3.8+                 |
| **ASGI Server**       | Uvicorn                     |

---

## 🏗 System Architecture

```
┌─────────────┐
│   Client    │
│ (Web/Mobile)│
└──────┬──────┘
       │ HTTP POST
       ▼
┌─────────────────────────────┐
│   FastAPI Application       │
│  ┌────────────────────────┐ │
│  │  /upload/ endpoint     │ │
│  └───────┬────────────────┘ │
│          │                  │
│          ▼                  │
│  ┌────────────────────────┐ │
│  │  OCR Processing        │ │
│  │  (pytesseract)         │ │
│  └───────┬────────────────┘ │
│          │                  │
│          ▼                  │
│  ┌────────────────────────┐ │
│  │  Field Extraction      │ │
│  │  (Regex Parsing)       │ │
│  └───────┬────────────────┘ │
└──────────┼──────────────────┘
           │
           ▼
    ┌─────────────┐
    │   MongoDB   │
    │  Database   │
    └─────────────┘
```

---

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Python**: Version 3.8 or higher
- **pip**: Python package installer
- **MongoDB**: Local instance or remote connection
- **Tesseract OCR**: System-level binary

### Installing Tesseract OCR

#### Windows

1. Download installer from [GitHub Releases](https://github.com/tesseract-ocr/tesseract/releases)
2. Run the installer (default path: `C:\Program Files\Tesseract-OCR\`)
3. Verify installation:
   ```cmd
   tesseract --version
   ```

#### macOS

```bash
brew install tesseract
tesseract --version
```

#### Ubuntu/Debian

```bash
sudo apt update
sudo apt install -y tesseract-ocr
tesseract --version
```

---

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Al-Powered_Identity_Verification_and_Fraud_Detection_for_KYC_Compliance
```

### 2. Create Virtual Environment (Recommended)

**Windows:**

```cmd
python -m venv .venv
.venv\Scripts\activate
```

**macOS/Linux:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

**Key Dependencies:**

- `fastapi` - Web framework
- `uvicorn[standard]` - ASGI server
- `python-multipart` - File upload support
- `pillow` - Image processing
- `pytesseract` - OCR wrapper
- `pymongo` - MongoDB driver

---

## ⚙️ Configuration

### Environment Variables

Create a `.env` file in the project root:

```env
# MongoDB Configuration
MONGO_URI=mongodb://localhost:27017
DB_NAME=kyc_database

# Tesseract Configuration (if not in PATH)
TESSERACT_CMD=C:\Program Files\Tesseract-OCR\tesseract.exe

# Optional: Upload Configuration
UPLOAD_DIR=./uploads
MAX_FILE_SIZE=10485760  # 10MB
```

### Setting Environment Variables

#### Windows (PowerShell - Persistent)

```powershell
[Environment]::SetEnvironmentVariable("TESSERACT_CMD", "C:\Program Files\Tesseract-OCR\tesseract.exe", "User")
[Environment]::SetEnvironmentVariable("MONGO_URI", "mongodb://localhost:27017", "User")
```

#### Windows (CMD - Persistent)

```cmd
setx TESSERACT_CMD "C:\Program Files\Tesseract-OCR\tesseract.exe"
setx MONGO_URI "mongodb://localhost:27017"
```

#### macOS/Linux (Temporary)

```bash
export TESSERACT_CMD=/usr/local/bin/tesseract
export MONGO_URI=mongodb://localhost:27017
```

#### macOS/Linux (Persistent)

Add to `~/.bashrc` or `~/.zshrc`:

```bash
export TESSERACT_CMD=/usr/local/bin/tesseract
export MONGO_URI=mongodb://localhost:27017
```

---

## 🎯 Usage

### Starting the Server

```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

**Options:**

- `--reload`: Auto-reload on code changes (development only)
- `--host 0.0.0.0`: Accept connections from any IP
- `--port 8000`: Run on port 8000

The API will be available at: `http://localhost:8000`

Interactive API docs: `http://localhost:8000/docs`

---

## 📡 API Documentation

### Endpoints

#### 1. Health Check

```http
GET /
```

**Response:**

```json
{
  "message": "KYC OCR Service is running",
  "status": "healthy"
}
```

#### 2. Upload Document

```http
POST /upload/
```

**Request:**

- Content-Type: `multipart/form-data`
- Field: `file` (image file)

**Supported Formats:** JPG, JPEG, PNG, PDF

**cURL Examples:**

**Linux/macOS:**

```bash
curl -X POST "http://localhost:8000/upload/" \
  -F "file=@/path/to/document.jpg"
```

**Windows (PowerShell):**

```powershell
curl.exe -X POST "http://localhost:8000/upload/" `
  -F "file=@C:\path\to\document.jpg"
```

**Python (requests):**

```python
import requests

url = "http://localhost:8000/upload/"
files = {"file": open("document.jpg", "rb")}
response = requests.post(url, files=files)
print(response.json())
```

**Response:**

```json
{
  "filename": "pan_card.jpg",
  "docType": "PAN",
  "rawText": "INCOME TAX DEPARTMENT\nPermanent Account Number Card\nABCDE1234F\nJOHN DOE\nFather's Name: RICHARD DOE\n01/01/1990",
  "parsed": {
    "panNumber": "ABCDE1234F",
    "aadhaarNumber": null,
    "name": "JOHN DOE",
    "fatherName": "RICHARD DOE",
    "dob": "01/01/1990",
    "gender": null,
    "address": null
  },
  "processingTimeMs": 342
}
```

### Document Type Detection

| Document    | Detected When                                          |
| ----------- | ------------------------------------------------------ |
| **PAN**     | Text contains "INCOME TAX" or "Permanent Account"      |
| **Aadhaar** | Text contains "UIDAI" or valid 12-digit Aadhaar number |
| **UNKNOWN** | No matching patterns found                             |

### Field Extraction Patterns

| Field          | Pattern                 | Example        |
| -------------- | ----------------------- | -------------- |
| PAN Number     | `[A-Z]{5}\d{4}[A-Z]`    | ABCDE1234F     |
| Aadhaar Number | `\d{4}\s?\d{4}\s?\d{4}` | 1234 5678 9012 |
| Date of Birth  | `\d{2}/\d{2}/\d{4}`     | 01/01/1990     |

---

## 💾 Database Schema

### Collections

#### `uploaded_documents`

```javascript
{
  "_id": ObjectId("..."),
  "filename": "pan_card.jpg",
  "docType": "PAN",
  "rawText": "OCR extracted text...",
  "parsed": {
    "panNumber": "ABCDE1234F",
    "aadhaarNumber": null,
    "name": "JOHN DOE",
    "fatherName": "RICHARD DOE",
    "dob": "01/01/1990",
    "gender": null,
    "address": null
  },
  "processingTimeMs": 342,
  "uploadedAt": ISODate("2024-01-15T10:30:00Z")
}
```

#### `users` (Future)

For user authentication and document association.

#### `kyc_data` (Future)

For comprehensive KYC verification records.

---

## 🧪 Testing

### Manual Testing

1. **Test PAN Card Upload:**

```bash
curl -X POST "http://localhost:8000/upload/" \
  -F "file=@samples/pan_card.jpg"
```

2. **Test Aadhaar Card Upload:**

```bash
curl -X POST "http://localhost:8000/upload/" \
  -F "file=@samples/aadhaar_card.jpg"
```

### Testing with Postman

1. Create new POST request to `http://localhost:8000/upload/`
2. Select Body → form-data
3. Add key `file` (type: File)
4. Choose image file
5. Send request

### Automated Testing (Future)

```bash
# Unit tests
pytest tests/

# With coverage
pytest --cov=app tests/
```

---

## 🔧 Troubleshooting

### Common Issues

#### 1. `TesseractNotFoundError`

**Problem:** Tesseract binary not found

**Solutions:**

- Verify installation: `tesseract --version`
- Add Tesseract to system PATH
- Set `TESSERACT_CMD` environment variable
- Uncomment the path setter in `app/main.py`:
  ```python
  pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'
  ```

#### 2. MongoDB Connection Error

**Problem:** Cannot connect to MongoDB

**Solutions:**

- Ensure MongoDB is running: `mongod --version`
- Check connection string in environment variables
- Verify network access if using remote MongoDB
- Check firewall settings

#### 3. Poor OCR Quality

**Problem:** Inaccurate text extraction

**Solutions:**

- **Image Quality:** Use high-resolution images (300+ DPI)
- **Preprocessing:** Convert to grayscale, apply thresholding
- **Format:** Use PNG or high-quality JPEG
- **Orientation:** Ensure document is properly aligned

**Image Preprocessing Example:**

```python
from PIL import Image, ImageEnhance

# Increase contrast
img = Image.open("document.jpg")
enhancer = ImageEnhance.Contrast(img)
img = enhancer.enhance(2.0)

# Convert to grayscale
img = img.convert('L')
img.save("preprocessed.jpg")
```

#### 4. File Upload Errors

**Problem:** File upload fails

**Check:**

- File size < 10MB (or configured limit)
- File format is supported (JPG, PNG, PDF)
- Correct form field name: `file`
- Content-Type header is set correctly

---

## 🗺 Roadmap

### Phase 1: Core Enhancements ✅

- [x] Basic OCR processing
- [x] PAN and Aadhaar parsing
- [x] MongoDB integration

### Phase 2: Security & Authentication 🚧

- [ ] JWT-based authentication
- [ ] User registration and login
- [ ] API rate limiting
- [ ] Request validation and sanitization

### Phase 3: Advanced Features 📋

- [ ] Cloud storage integration (AWS S3/Azure Blob)
- [ ] ML-based fraud detection
- [ ] Face detection and matching
- [ ] Document authenticity verification
- [ ] Liveness detection
- [ ] Multi-language OCR support

### Phase 4: Production Ready 📋

- [ ] Comprehensive logging (structured logs)
- [ ] Performance monitoring
- [ ] Docker containerization
- [ ] CI/CD pipeline
- [ ] Horizontal scaling support
- [ ] Comprehensive test suite (>80% coverage)

### Phase 5: Additional Features 📋

- [ ] Webhook notifications
- [ ] Bulk upload processing
- [ ] Dashboard and analytics
- [ ] Export functionality (PDF reports)
- [ ] Audit trail and compliance logs

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/AmazingFeature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add some AmazingFeature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/AmazingFeature
   ```
5. **Open a Pull Request**

### Code Style

- Follow PEP 8 guidelines
- Add docstrings to functions
- Include type hints
- Write unit tests for new features

---

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## 📞 Support & Contact

For questions, issues, or suggestions:

- **Issues**: [GitHub Issues](https://github.com/yourusername/repository/issues)
- **Documentation**: Check the `/docs` endpoint when the server is running
- **Email**: your.email@example.com

---

## 🙏 Acknowledgments

- [FastAPI](https://fastapi.tiangolo.com/) - Modern web framework
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) - OCR engine
- [MongoDB](https://www.mongodb.com/) - Database solution

---

**⭐ If you find this project useful, please consider giving it a star!**
