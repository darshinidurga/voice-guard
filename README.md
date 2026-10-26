# 🛡️ VoiceGuard: Real-Time AI Voice Cloning & Fraud Detection System

<p align="center">
  <img src="https://img.shields.io/badge/SIH-Problem%2026104-blueviolet?style=for-the-badge&logo=shield" alt="SIH Problem" />
  <img src="https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white" alt="Python Version" />
  <img src="https://img.shields.io/badge/PyTorch-2.x-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch" />
  <img src="https://img.shields.io/badge/FastAPI-0.141-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/Wav2Vec-2.0-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black" alt="Hugging Face" />
  <img src="https://img.shields.io/badge/Faster--Whisper-ASR-orange?style=for-the-badge&logo=openai&logoColor=white" alt="Faster-Whisper" />
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge" alt="Status" />
</p>

<p align="center">
  <strong>An intelligent multi-modal defense framework designed to detect synthesized deepfake voices and social engineering phone scams in real time.</strong>
</p>

---

## 📌 Executive Summary

With the explosive rise of generative audio models (Bark, XTTS, ElevenLabs, VALL-E), voice cloning has become a weapon of choice for cybercriminals conducting **financial fraud, CEO impersonation, and family emergency extortion scams**. Traditional telephony defenses fail because they inspect only caller ID or metadata.

**VoiceGuard** solves this critical security gap by deploying a **Dual-Engine Fusion Architecture**:
1. **Acoustic Deepfake Detector**: Inspects micro-spectral anomalies and vocoder artifacts using **Wav2Vec 2.0 + Bi-directional LSTM with Attention Pooling**.
2. **Semantic Fraud & Urgency Engine**: Rapidly transcribes conversations via quantized **Faster-Whisper** and performs real-time NLP classification to detect urgency cues, credential phishing, money transfer demands, and social engineering manipulation.
3. **Multi-Modal Risk Engine**: Fuses acoustic spoof probability with conversational context to classify call threats as `Low`, `Medium`, or `High`, triggering instant defensive intervention or verification challenges.

---

## ⚡ Key Highlights

- 🎙️ **Dual-Engine Protection**: Combines neural acoustic feature inspection with natural language behavioral threat modeling.
- ⚡ **Low-Latency Inference**: 3-second windowing pipeline optimized for streaming call audio.
- 🧠 **Attention-Guided BiLSTM**: Captures temporal prosodic inconsistencies across raw audio representations.
- 🔍 **Real-Time NLP Heuristics**: Detects OTP theft, wire transfer requests, banking probes, gift card scams, and artificial urgency.
- 📊 **SOC-Grade Security Dashboard**: Cyberpunk-themed real-time analyst console displaying live waveforms, confidence meters, threat gauges, and dynamic transcripts.
- 🎬 **Controlled Demo Mode**: Built-in demonstration harness designed for live hackathon presentations and field testing.

---

## 🏗️ Architecture & Pipeline

```mermaid
flowchart TD
    A([🎙️ Live Audio Stream / Upload]) --> B[Audio Preprocessor<br/>16kHz Mono / 3s Chunks]

    subgraph Dual Engine Analysis
        B -->|Raw Audio Waveform| C[Acoustic Deepfake Engine]
        B -->|Quantized Speech| D[Semantic NLP Engine]

        subgraph C [Acoustic Branch]
            C1[facebook/wav2vec2-base-960h] --> C2[Bi-directional LSTM (hidden=128)]
            C2 --> C3[Attention Pooling Layer]
            C3 --> C4[MLP Classifier + Dropout]
            C4 --> C5[Voice Authenticity Score]
        end

        subgraph D [Semantic Branch]
            D1[Faster-Whisper ASR Model] --> D2[Live Transcript Stream]
            D2 --> D3[Social Engineering Pattern Engine]
            D3 --> D4[Urgency & Phishing Scorer]
        end
    end

    C5 --> E{Multi-Modal Risk Engine}
    D4 --> E

    E --> F[Threat Level: LOW / MEDIUM / HIGH]
    E --> G[Trigger Identity Challenge / Alert]

    F --> H[🖥️ SOC Real-Time Web Dashboard]
    D2 --> H
```

---

## 🔬 Model Deep Dive: V2-A Acoustic Architecture

VoiceGuard replaces legacy hand-crafted spectrograms (MFCC/CQCC) with self-supervised latent acoustic representations that expose high-order vocoder artifacts.

```
Input Audio [16 kHz, 3s]
   │
   ▼
Wav2Vec 2.0 Base (Feature Extractor)
   │  Output: [Batch, Time, 768]
   ▼
Bi-directional LSTM (hidden_size=128, bidirectional=True)
   │  Captures temporal dependencies across 256 feature dimensions
   ▼
Attention Pooling
   │  Computes softmax weights across time steps to highlight spoof artifacts
   ▼
Dense Classifier
   │  Linear(256 -> 64) -> ReLU -> Dropout(0.30) -> Linear(64 -> 1)
   ▼
Sigmoid / Logit Output -> Spoof Probability Score
```

---

## 📂 Repository Structure

```plaintext
voiceguard/
│
├── app.py                            # FastAPI backend with static file server & endpoints
├── voiceguard_pipeline.py            # End-to-end integration pipeline (Audio + ASR + ML)
├── risk_engine.py                    # Multi-modal acoustic & semantic risk fusion
├── scam_detector.py                  # Rule-based and semantic fraud/urgency detector
├── requirements.txt                  # Production dependencies
│
├── frontend/                         # Modern SOC Dashboard UI
│   ├── index.html                    # Main SOC dashboard
│   ├── style.css                     # Glassmorphic dark security theme
│   ├── app.js                        # Audio recording and WebSocket/REST client
│   ├── demo.html                     # Competition presentation demo interface
│   ├── demo.css                      # Demo styling
│   └── demo.js                       # Demo interaction logic
│
├── ml_rebuild/                       # Model Training & Evaluation Suite
│   ├── models/
│   │   └── voiceguard_v2a.pth        # Trained V2-A PyTorch model checkpoint
│   ├── training/
│   │   ├── train_v2.py               # V2-A training script with WeightedRandomSampler
│   │   ├── evaluate_v2.py            # Comprehensive evaluation benchmark
│   │   ├── threshold_v2.py           # Optimal decision threshold sweeps
│   │   ├── extract_train_embeddings.py
│   │   ├── extract_val_embeddings.py
│   │   ├── prepare_memmap.py         # High-throughput memory-mapped data loader
│   │   └── realtime_detector.py      # Standalone real-time stream detector
│   ├── audit_dataset.py              # Data sanity and balance verification
│   └── make_speaker_split.py         # Zero-leakage speaker split generator
│
└── README.md                         # Project documentation
```

---

## 🚀 Quickstart Guide

### 1. Prerequisites
- **Python**: Version 3.10 or higher
- **FFmpeg**: Required for audio transcoding (`winget install Gyan.FFmpeg` on Windows, `sudo apt install ffmpeg` on Ubuntu/Debian)
- **Git**

### 2. Clone the Repository
```bash
git clone https://github.com/darshinidurga/sih26104-voice-guard.git
cd sih26104-voice-guard
```

### 3. Create a Virtual Environment
```bash
# Windows
python -m venv .venv
.venv\Scripts\activate

# macOS / Linux
python3 -m venv .venv
source .venv/bin/activate
```

### 4. Install Dependencies
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 5. Launch the Application
```bash
uvicorn app:app --host 0.0.0.0 --port 8000 --reload
```

Open your browser and navigate to:
- **SOC Security Dashboard**: `http://localhost:8000/`
- **Presentation Demo Console**: `http://localhost:8000/demo`
- **API Documentation**: `http://localhost:8000/docs`

---

## 📡 API Reference

### Analyze Audio Stream / File
`POST /demo/analyze`

**Request:** `multipart/form-data`
- `file`: Audio file (`.wav`, `.mp3`, etc.)
- `source`: `"microphone"` | `"upload"`

**Sample Response:**
```json
{
  "voice_classification": "SYNTHETIC / CLONED VOICE",
  "voice_confidence": 0.98,
  "is_fake": true,
  "transcript": "Hello, this is your bank manager. Your account is compromised. Send me the OTP immediately.",
  "scam_score": 0.85,
  "risk_level": "high",
  "urgency_detected": true,
  "matched_phrases": [
    "send me the otp",
    "account compromised",
    "immediately"
  ],
  "trigger_challenge": true
}
```

### System Health
`GET /health`
```json
{
  "status": "ok"
}
```

---

## 🛡️ Social Engineering Detection Categories

VoiceGuard's semantic engine evaluates conversational speech across five critical threat dimensions:

| Category | Indicators & Triggers | Threat Weight |
|:---|:---|:---:|
| 💳 **Financial Demands** | "send money", "transfer funds", "wire payment" | High |
| 🔑 **Credential Phishing** | "OTP", "verification code", "password", "CVV", "PIN" | Critical |
| 🏦 **Account Exploitation** | "bank details", "account blocked", "credit card" | High |
| 🎁 **Unusual Payment Rails**| "gift card", "crypto deposit", "voucher" | High |
| ⏱️ **Artificial Urgency** | "immediately", "right now", "urgent", "don't wait" | Multiplier |

---

## 🏆 Hackathon Details

- **Event**: Smart India Hackathon (SIH)
- **Problem Statement ID**: 26104
- **Title**: Voice Guard - AI Voice Cloning & Social Engineering Detection
- **Author**: Darshini Durga ([@darshinidurga](https://github.com/darshinidurga))

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).
