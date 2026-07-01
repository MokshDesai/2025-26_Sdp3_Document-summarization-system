# Document Summarization System (DSS)

<div align="center">

**An intelligent document processing platform that extracts text from PDFs and DOCX files and generates concise summaries using advanced NLP techniques.**

![Python](https://img.shields.io/badge/Python-3.9+-blue?style=flat-square)
![Django](https://img.shields.io/badge/Django-4.2-darkgreen?style=flat-square)
![React](https://img.shields.io/badge/React-19.2-61DAFB?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [System Architecture](#system-architecture)
- [Installation & Setup](#installation--setup)
- [Configuration](#configuration)
- [Usage Guide](#usage-guide)
- [API Documentation](#api-documentation)
- [Project Structure](#project-structure)
- [Advanced Features](#advanced-features)
- [Future Enhancements](#future-enhancements)
- [Troubleshooting](#troubleshooting)

---

## 🎯 Overview

The **Document Summarization System** is a full-stack web application that automates the process of extracting meaningful information from documents. Users can upload PDF or DOCX files, and the system intelligently extracts text using multiple methods (standard extraction, OCR for scanned documents, and image captioning) before generating concise summaries using a local LLM.

### Key Use Cases

- **Business Intelligence**: Quickly summarize reports and documents
- **Research**: Extract and summarize academic papers
- **Legal**: Review and summarize contracts and agreements
- **Content Management**: Organize large document repositories

---

## ✨ Key Features

### 📁 Multi-Format Document Support

- ✅ **PDFs** (text-based and scanned)
- ✅ **DOCX** files (Microsoft Word)
- ✅ **Hybrid Processing** for mixed-content documents

### 🔍 Advanced Text Extraction

| Method               | Use Case                                    |
| -------------------- | ------------------------------------------- |
| **PyPDF2**           | Standard text extraction from digital PDFs  |
| **python-docx**      | DOCX file parsing and text extraction       |
| **Tesseract OCR**    | Text recognition from scanned PDFs & images |
| **Image Captioning** | Context extraction from document images     |

### 🤖 Intelligent Summarization

- **Local LLM Integration** via Ollama (no external API calls)
- **Context-Aware Summaries** with structured formatting
- **Configurable Models** (supports Mistral, Llama 2, and more)
- **Caching System** for optimized performance

### 👤 User Management & Authentication

- Email/password registration and login
- Google OAuth 2.0 integration
- Session-based authentication
- Profile management
- Secure password change with OTP verification

### 💳 Credit-Based System

- User credit allocation (100 credits on signup)
- Per-document credit consumption
- Razorpay payment integration for credit top-ups
- Transaction history and billing management

### 📊 Document Management

- Document upload and storage
- Extraction status tracking
- Summary storage and retrieval
- Download capabilities for processed documents
- User-specific document history

---

## 🛠 Tech Stack

### Backend

| Category             | Technology                       |
| -------------------- | -------------------------------- |
| **Framework**        | Django 4.2.27                    |
| **API**              | Django REST Framework            |
| **Database**         | SQLite3 (with Django ORM)        |
| **Authentication**   | OAuth 2.0, Session-based         |
| **Text Extraction**  | PyPDF2, python-docx, pytesseract |
| **Image Processing** | pdf2image, Pillow                |
| **NLP/LLM**          | Ollama (local), transformers     |
| **Payment Gateway**  | Razorpay SDK                     |

### Frontend

| Category        | Technology      |
| --------------- | --------------- |
| **Framework**   | React 19.2      |
| **Build Tool**  | Vite 7.2        |
| **Routing**     | React Router v7 |
| **Styling**     | CSS3            |
| **HTTP Client** | Fetch API       |

### Infrastructure & DevOps

- **Python Environment**: Virtual Environment (venv)
- **Package Manager**: pip
- **Version Control**: Git

---

## 🏗 System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      USER BROWSER                            │
│  ┌────────────────────────────────────────────────────────┐  │
│  │          React Frontend (Vite)                          │  │
│  │  - File Upload Interface                               │  │
│  │  - Authentication (Login/Signup)                        │  │
│  │  - Document Management                                 │  │
│  │  - Summary Display & Download                          │  │
│  └────────────────────────────────────────────────────────┘  │
└──────────────────────┬──────────────────────────────────────┘
                       │ (HTTPS/Fetch API)
                       │
┌──────────────────────▼──────────────────────────────────────┐
│               DJANGO WEB SERVER                              │
│  ┌────────────────────────────────────────────────────────┐  │
│  │ API Endpoints (views.py)                               │  │
│  │  - Authentication (/api/auth/*)                        │  │
│  │  - File Upload (/api/summarize/)                       │  │
│  │  - Document Management (/api/uploads/*)                │  │
│  │  - Payments (/api/payments/*)                          │  │
│  └────────────────────────────────────────────────────────┘  │
│  ┌────────────────────────────────────────────────────────┐  │
│  │ Processing Modules                                      │  │
│  │  - Text Extraction (multiple methods)                  │  │
│  │  - OCR Engine (pytesseract)                             │  │
│  │  - Image Captioning (transformers)                     │  │
│  │  - Summarization (Ollama integration)                  │  │
│  │  - Caching System (in-memory LRU)                      │  │
│  └────────────────────────────────────────────────────────┘  │
└──────────────────────┬──────────────────────────────────────┘
                       │
        ┌──────────────┼──────────────┐
        │              │              │
┌───────▼──────┐ ┌────▼────────┐ ┌───▼──────────┐
│  SQLite DB   │ │ Ollama LLM  │ │ Razorpay API │
│              │ │             │ │              │
│ - Users      │ │ - Mistral   │ │ - Payments   │
│ - Documents  │ │ - Llama 2   │ │ - Webhooks   │
│ - Credits    │ │ - Others    │ │              │
└──────────────┘ └─────────────┘ └──────────────┘
```

---

## 🚀 Installation & Setup

### Prerequisites

- **Python 3.9+**
- **pip** (Python package manager)
- **Node.js 16+** (for frontend)
- **Ollama** (for local LLM summarization)
- **Tesseract OCR** (for scanned PDF processing)

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/Document_summarization_system.git
cd Document_summarization_system
```

### Step 2: Backend Setup

#### 2.1 Create Virtual Environment

```bash
# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

#### 2.2 Install Python Dependencies

```bash
cd Document_summarizaton_system

# Install all required packages
pip install -r requirements.txt

# If installation fails, install individually:
pip install Django==4.2.27
pip install PyPDF2==3.0.1
pip install python-docx==1.2.0
pip install pytesseract==0.3.13
pip install pdf2image==1.17.0
pip install pillow==11.3.0
pip install transformers
pip install torch
pip install ollama==0.4.5
pip install razorpay==1.4.2
pip install python-dotenv==1.1.0
```

#### 2.3 Install System Dependencies

**For macOS:**

```bash
# Install Tesseract OCR
brew install tesseract

# Install pdf2image dependencies
brew install poppler
```

**For Ubuntu/Debian:**

```bash
sudo apt-get update
sudo apt-get install tesseract-ocr
sudo apt-get install poppler-utils
```

**For Windows:**

- Download Tesseract installer from: https://github.com/UB-Mannheim/tesseract/wiki
- Download Poppler from: http://blog.alivate.com.au/poppler-windows/

#### 2.4 Setup Ollama (Local LLM)

```bash
# Download and install Ollama from: https://ollama.com

# Start Ollama service
ollama serve

# In another terminal, pull a model (one-time setup)
ollama pull mistral
# or
ollama pull llama2
```

#### 2.5 Configure Environment Variables

Create a `.env` file in the `Document_summarizaton_system` directory:

```env
# Django Settings
DEBUG=True
SECRET_KEY=your-secret-key-here
ALLOWED_HOSTS=localhost,127.0.0.1

# Database
DB_ENGINE=django.db.backends.sqlite3
DB_NAME=db.sqlite3

# Ollama Configuration
DSS_OLLAMA_MODEL=mistral
DSS_OLLAMA_HOST=http://localhost:11434
DSS_SUMMARY_CACHE_MAX_ITEMS=24

# Email Configuration (for OTP)
EMAIL_BACKEND=django.core.mail.backends.console.EmailBackend
DEFAULT_FROM_EMAIL=noreply@documentsummarizer.com

# Google OAuth (optional)
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
GOOGLE_REDIRECT_URI=http://localhost:8000/api/auth/google/callback/

# Razorpay (for payments)
RAZORPAY_KEY_ID=your-razorpay-key-id
RAZORPAY_KEY_SECRET=your-razorpay-key-secret

# Tesseract OCR
TESSERACT_PATH=/usr/bin/tesseract  # macOS: /usr/local/bin/tesseract
```

#### 2.6 Initialize Database

```bash
# Apply migrations
python manage.py migrate

# Create superuser (optional, for admin panel)
python manage.py createsuperuser
```

### Step 3: Frontend Setup

```bash
cd ../frontend

# Install Node.js dependencies
npm install

# Build frontend
npm run build

# For development (optional):
npm run dev
```

### Step 4: Run the Application

#### Terminal 1: Start Django Backend

```bash
cd Document_summarizaton_system
source venv/bin/activate
python manage.py runserver
# Server runs on http://localhost:8000
```

#### Terminal 2: Ensure Ollama is Running

```bash
ollama serve
# Ollama listens on http://localhost:11434
```

#### Terminal 3: Serve Frontend (Development)

```bash
cd frontend
npm run dev
# Frontend runs on http://localhost:5173 (Vite default)
```

---

## ⚙️ Configuration

### Key Configuration Files

| File             | Purpose                                   |
| ---------------- | ----------------------------------------- |
| `settings.py`    | Django settings, database, installed apps |
| `urls.py`        | URL routing configuration                 |
| `vite.config.js` | Frontend build and dev server config      |
| `.env`           | Environment variables (create manually)   |

### Database Models

```
User (Django built-in)
├── StoredDocument
│   ├── original_name
│   ├── extracted_text
│   ├── summary
│   └── created_at
├── UserCredits
│   ├── credits
│   └── updated_at
└── RazorpayTopupOrder
    ├── razorpay_order_id
    ├── status (created/paid/failed)
    ├── credits_to_add
    └── amount_paise
```

---

## 💻 Usage Guide

### 1. User Registration

```bash
POST /api/auth/signup/
Content-Type: application/json

{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "SecurePassword123"
}
```

### 2. Upload and Summarize Document

```bash
POST /api/summarize/
Content-Type: multipart/form-data

{
  "file": <binary PDF/DOCX file>,
  "summarization_level": "medium"  # or "short", "detailed"
}
```

### 3. Retrieve Summary

```bash
GET /api/uploads/{upload_id}/
```

### 4. List User's Documents

```bash
GET /api/uploads/
```

### 5. Process Payment

```bash
POST /api/payments/razorpay/create-order/
Content-Type: application/json

{
  "plan_id": "plan_100",
  "credits_to_add": 100
}
```

---

## 📡 API Documentation

### Authentication Endpoints

| Method | Endpoint                     | Description           |
| ------ | ---------------------------- | --------------------- |
| POST   | `/api/auth/signup/`          | Register new user     |
| POST   | `/api/auth/login/`           | User login            |
| GET    | `/api/auth/me/`              | Get current user info |
| GET    | `/api/auth/logout/`          | Logout user           |
| POST   | `/api/auth/google/login/`    | Google OAuth login    |
| POST   | `/api/auth/profile/`         | Update user profile   |
| POST   | `/api/auth/change-password/` | Change password       |
| POST   | `/api/auth/delete-account/`  | Delete account        |

### Document Processing Endpoints

| Method | Endpoint                       | Description                   |
| ------ | ------------------------------ | ----------------------------- |
| POST   | `/api/summarize/`              | Upload and summarize document |
| GET    | `/api/summarize/stream/`       | Stream summary (real-time)    |
| POST   | `/api/uploads/preflight/`      | Check upload eligibility      |
| GET    | `/api/uploads/`                | List all user uploads         |
| GET    | `/api/uploads/{id}/`           | Get specific upload details   |
| GET    | `/api/uploads/{id}/download/`  | Download document             |
| POST   | `/api/uploads/{id}/summarize/` | Re-summarize existing upload  |

### Payment Endpoints

| Method | Endpoint                               | Description          |
| ------ | -------------------------------------- | -------------------- |
| GET    | `/api/payments/razorpay/config/`       | Get Razorpay config  |
| POST   | `/api/payments/razorpay/create-order/` | Create payment order |
| POST   | `/api/payments/razorpay/verify/`       | Verify payment       |

---

## 📁 Project Structure

```
Document_summarization_system/
├── README.md
├── requirements.txt
├── db.sqlite3
├── manage.py
│
├── Document_summarizaton_system/          # Django project settings
│   ├── settings.py                         # Main configuration
│   ├── urls.py                             # URL routing
│   ├── wsgi.py                             # WSGI application
│   ├── asgi.py                             # ASGI application
│   └── __init__.py
│
├── DSS_app/                                # Main application
│   ├── models.py                           # Database models
│   ├── views.py                            # API endpoints
│   ├── urls.py                             # App URL patterns
│   ├── middleware.py                       # Custom middleware
│   ├── summarization.py                    # Ollama integration
│   ├── image_captioning.py                 # Image-to-text module
│   ├── admin.py                            # Django admin config
│   ├── apps.py                             # App configuration
│   ├── tests.py                            # Unit tests
│   ├── migrations/                         # Database migrations
│   │   └── 0001_initial.py
│   └── management/
│       └── commands/                       # Custom management commands
│
├── frontend/                               # React application
│   ├── package.json                        # Node.js dependencies
│   ├── vite.config.js                      # Vite build config
│   ├── eslint.config.js                    # ESLint rules
│   ├── index.html                          # Entry HTML
│   └── src/
│       ├── main.jsx                        # React entry point
│       ├── App.jsx                         # Root component
│       ├── App.css
│       ├── components/
│       │   ├── AuthShell.jsx               # Auth wrapper
│       │   ├── RequireAuth.jsx             # Protected routes
│       │   ├── SiteChrome.jsx              # Layout component
│       │   └── Icons.jsx                   # Icon library
│       ├── pages/
│       │   ├── Home.jsx                    # Home page
│       │   ├── Upload.jsx                  # Document upload
│       │   ├── MyUploads.jsx               # Document history
│       │   ├── Login.jsx                   # Login page
│       │   ├── Signup.jsx                  # Registration
│       │   ├── Profile.jsx                 # User profile
│       │   ├── Billing.jsx                 # Payment page
│       │   └── ...
│       └── lib/
│           ├── auth.js                     # Auth utilities
│           └── userSession.js              # Session management
│
└── learning/                               # Learning resources
    └── (Documentation & examples)
```

---

## 🔧 Advanced Features

### 1. Multi-Method Text Extraction

The system uses a fallback chain for robust text extraction:

```python
# Priority 1: Standard PDF text extraction
PyPDF2 → pdfplumber

# Priority 2: OCR for scanned documents
pytesseract → Tesseract

# Priority 3: Image captioning for visual content
transformers (Vision-to-Text model)
```

### 2. Caching System

- **In-Memory LRU Cache** for summaries
- **Configurable cache size**: `DSS_SUMMARY_CACHE_MAX_ITEMS`
- Reduces redundant LLM calls
- Thread-safe implementation

### 3. Streaming Responses

Real-time summary streaming for large documents:

```javascript
// Frontend usage
fetch("/api/summarize/stream/", { method: "POST" })
  .then((response) => response.body.getReader())
  .then((reader) => {
    const readChunk = ({ done, value }) => {
      if (done) return;
      console.log(new TextDecoder().decode(value));
      return reader.read().then(readChunk);
    };
    return reader.read().then(readChunk);
  });
```

### 4. Credit System

- Users start with **100 credits**
- Each document costs credits based on file size
- Razorpay integration for top-ups
- Real-time credit balance tracking

---

## 🚀 Future Enhancements

### Phase 2 Features

- [ ] Support for additional file formats (XLSX, PPT, TXT)
- [ ] Multiple language support
- [ ] Batch document processing
- [ ] Advanced analytics dashboard
- [ ] Document comparison and clustering
- [ ] Email notifications for processing completion

### Performance Optimizations

- [ ] Elasticsearch integration for document search
- [ ] Redis caching layer
- [ ] Celery for async task processing
- [ ] Database query optimization
- [ ] CDN integration for frontend assets

### Security Enhancements

- [ ] Two-factor authentication (2FA)
- [ ] Rate limiting on API endpoints
- [ ] Advanced encryption for stored documents
- [ ] IP whitelist functionality
- [ ] Audit logging for user actions

### ML/AI Improvements

- [ ] Fine-tuned models for domain-specific summaries
- [ ] Multi-language summarization
- [ ] Fact extraction and verification
- [ ] Sentiment analysis
- [ ] Key phrase extraction

---

## 🐛 Troubleshooting

### Issue: "Ollama connection refused"

```
Error: Connection refused at http://localhost:11434
```

**Solution:**

```bash
# Ensure Ollama is running
ollama serve

# Check if it's running on different port
lsof -i :11434
```

### Issue: "Tesseract not found"

```
Error: pytesseract.TesseractNotFoundError
```

**Solution:**

```bash
# macOS
brew install tesseract

# Linux (Ubuntu/Debian)
sudo apt-get install tesseract-ocr

# Update settings with correct path
TESSERACT_PATH=/path/to/tesseract
```

### Issue: "Out of memory during PDF processing"

**Solution:**

- Process large files in chunks
- Increase system RAM
- Adjust Ollama thread count: `DSS_OLLAMA_NUM_THREADS`

### Issue: "CORS errors in frontend"

**Solution:**
Add to Django settings:

```python
CORS_ALLOWED_ORIGINS = [
    "http://localhost:5173",
    "http://localhost:3000",
]
```

### Issue: "Database locked"

**Solution:**

```bash
# SQLite locking issue
# Kill existing processes
pkill -f "python manage.py runserver"

# Reset database (caution: deletes data)
rm db.sqlite3
python manage.py migrate
```

---

## 📚 Additional Resources

- [Django Documentation](https://docs.djangoproject.com/)
- [React Documentation](https://react.dev/)
- [Ollama Documentation](https://ollama.com/)
- [Razorpay API Docs](https://razorpay.com/docs/)
- [Tesseract OCR Guide](https://tesseract-ocr.github.io/)

---

## 📝 License

This project is licensed under the MIT License - see LICENSE file for details.

---

## 👨‍💻 Author

**Moksh Desai**  
GitHub: [@mokshdesai](https://github.com/mokshdesai)

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 💬 Support

For questions or issues, please open a GitHub issue or contact the project maintainer.

---

**Made with ❤️ for SDP 3 (2025-26)**

        Django Frontend (HTML + JavaScript)

Django Backend (views.py)

        Django Backend (views.py)

Text Extraction (PDF / DOCX / OCR)

        Text Extraction (PDF / DOCX / OCR)

Text Cleaning & Chunking

        Text Cleaning & Chunking

Summarization Model (BART – local)

        Summarization Model (BART – local)

Summary Displayed to User

         Summary Displayed to User
