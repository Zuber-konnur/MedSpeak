# 🩺 MedSpeak Clinical Assistant

MedSpeak Clinical Assistant is an intelligent, high-efficiency healthcare automation platform designed to convert post-operative audio dictations or uploaded surgical notes into structured, validated, and cryptographically secure medical reports.

The platform combines:
- 🧠 Local quantized medical LLMs
- ☁️ Cloud-based generative AI
- ⚙️ Rule-based NLP fallback extraction

This architecture ensures **high availability**, **offline resilience**, and **clinical-grade document consistency** even in low-connectivity healthcare environments.

---

# 🚀 Features

## 🔄 Tiered Fallback Extraction Pipeline

MedSpeak automatically switches extraction engines depending on hardware availability, API access, or offline conditions:

```math
MedGemma (Local 4-bit)
        ↓
Gemini 2.5 Flash (Cloud)
        ↓
Rule-Based NLP Engine (spaCy)
```

### Processing Flow

1. **Primary Layer — MedGemma 1.5 4B**
   - Local quantized inference (NF4 / 4-bit)
   - GPU optimized
   - Fully offline capable

2. **Secondary Layer — Gemini 2.5 Flash**
   - Cloud-based structured medical extraction
   - Fast schema-constrained responses

3. **Final Fallback — Rule-Based NLP**
   - spaCy Matcher pipelines
   - SymSpell correction engine
   - Regex + token normalization
   - Zero dependency on external AI services

---

# 🧠 Advanced Medical NLP Engine

## ✨ Intelligent Transcription Cleanup

The NLP layer includes:

- **SymSpell medical-aware correction**
- Preservation of:
  - Drug names
  - Anatomical terminology
  - Surgical procedures
  - Clinical abbreviations

### Example

**Input**
```text
patient bp one ten over eighty pulse ninety eight
```

**Output**
```text
BP: 110/80
Pulse: 98 bpm
```

---

# 🔐 Cryptographic Report Integrity

Every generated `MedicalReport` includes:

- SHA-256 checksum hashing
- Payload integrity verification
- Tamper-resistance tracking

## Security Design

The hashing pipeline isolates:
- Runtime metadata
- AI model metadata
- Clinical payload data

This prevents:
- False checksum invalidation
- Non-clinical changes corrupting signatures

---

# 📄 Automated Clinical PDF Generation

MedSpeak generates standardized corporate-style reports using **ReportLab**.

### Features
- Structured surgical summaries
- Professional healthcare formatting
- Instant PDF compilation
- Searchable historical reports
- Frontend indexing system

---

# 🏗️ System Architecture

```text
  [ Clinician Dictation ] ---> Audio Stream / File Upload (.webm, .mp3, .wav)
                                      |
                                      v
                        [ Faster-Whisper Transcription ]
                                      |
       +------------------------------+------------------------------+
       |                              |                              |
       v                              v                              v
[ MedGemma 1.5 4B ]          [ Gemini 2.5 Flash ]          [ Enhanced Rule Engine ]
(Local Quantized NF4)         (Cloud API Pipeline)           (spaCy & Token Matcher)
       |                              |                              |
       +------------------------------+------------------------------+
                                      |
                                      v
                         [ JSON Schema Validation ]
                                      |
                                      v
                      [ SHA-256 Checksum Generation ]
                                      |
             +------------------------+------------------------+
             |                                                 |
             v                                                 v
   [ Structured JSON Storage ]                        [ ReportLab PDF Layout ]
```

---

# 📦 Project Structure

```text
medspeak-assistant/
│
├── models/
│   ├── __init__.py
│   ├── loaders.py
│   └── medical_report.py
│
├── utils/
│   ├── transcription.py
│   ├── extraction.py
│   ├── rule_based_extractor.py
│   └── pdf_generator.py
│
├── static/
│   ├── style.css
│   └── script.js
│
├── templates/
│   └── index.html
│
├── generated_pdfs/
├── generated_reports/
│
└── main.py
```

---

# ⚙️ Technology Stack

## Backend
- FastAPI
- Uvicorn
- Transformers
- Faster-Whisper
- Google Generative AI
- spaCy
- SymSpellPy
- ReportLab

## AI / NLP
- MedGemma 1.5 4B
- Gemini 2.5 Flash
- SciSpaCy
- NF4 Quantization
- Rule-Based Clinical Extraction

## Frontend
- HTML5
- CSS3
- JavaScript
- Responsive Dashboard UI

---

# 🛠️ Installation

## 1. Clone Repository

```bash
git clone https://github.com/your-org/medspeak-assistant.git

cd medspeak-assistant
```

---

## 2. Install Dependencies

```bash
pip install fastapi uvicorn transformers bitsandbytes faster-whisper reportlab jinja2 python-multipart pyngrok accelerate huggingface_hub google-generativeai symspellpy word2number python-dateutil scispacy
```

---

## 3. Install spaCy Model

```bash
python -m spacy download en_core_web_sm
```

---

# ▶️ Running the Application

## Local Development

```bash
uvicorn main:app --host 0.0.0.0 --port 8000 --log-level info
```

Application will be available at:

```text
http://localhost:8000
```

---

# ☁️ Google Colab / Remote GPU Deployment

```python
from huggingface_hub import login
from pyngrok import ngrok

HF_TOKEN = "your_hf_token_here"
NGROK_TOKEN = "your_ngrok_token_here"

login(token=HF_TOKEN)
ngrok.set_auth_token(NGROK_TOKEN)

public_url = ngrok.connect(8000).public_url

print(f"🌐 MEDSPEAK IS LIVE AT: {public_url}")

!uvicorn main:app --host 0.0.0.0 --port 8000
```

---

# 🧾 Clinical Extraction Pipeline

## Step 1 — Audio Input
Supported formats:
- `.wav`
- `.mp3`
- `.webm`

## Step 2 — Whisper Transcription
- Speaker-aware segmentation
- Noise-tolerant transcription
- Medical phrase optimization

## Step 3 — Structured Extraction
- AI schema enforcement
- Entity normalization
- Numerical phrase conversion

## Step 4 — Validation
- JSON schema verification
- Field normalization
- Missing-field detection

## Step 5 — Report Output
- JSON archival
- PDF generation
- SHA-256 signature attachment

---

# 🔒 Security & Compliance

## Metadata Isolation
Runtime system metadata is separated from patient payloads during cryptographic hashing.

## Integrity Validation
Every generated report includes:
- SHA-256 integrity signature
- Timestamp validation
- Structured schema tracking

## Offline Capability
The local extraction layer ensures:
- Zero cloud dependency
- Offline hospital deployment
- Fail-safe fallback operation

---

# 📸 Future Roadmap

- [ ] HL7 / FHIR integration
- [ ] Multi-language dictation support
- [ ] Real-time operating room transcription
- [ ] Clinical ICD-10 auto-coding
- [ ] Dockerized enterprise deployment
- [ ] Role-based authentication system
- [ ] PACS integration support

---

# 🧪 Example Use Cases

- Post-operative surgical summaries
- Emergency room dictation automation
- Clinical discharge documentation
- Outpatient procedure reporting
- Voice-assisted EHR drafting

---

# 📜 License

This project is proprietary and intended solely for:
- Clinical research
- Automation evaluation
- Technical demonstration

Production medical deployment requires formal review, validation, and regulatory compliance assessment.

---

# 👨‍⚕️ Disclaimer

MedSpeak Clinical Assistant is an assistive documentation system and must not replace licensed medical judgment, diagnosis, or clinical decision-making.

All generated reports should be reviewed by qualified healthcare professionals before official use.
