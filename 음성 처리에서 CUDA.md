# CUDA로 가속하는 음성 처리 시스템 🎧⚡

## 🧾 개요
CUDA는 NVIDIA GPU의 병렬 연산 능력을 활용하여 **음성 인식(STT), 음성 합성(TTS), 음성 분리, 특징 추출 등** 다양한 음성 처리 작업을 **대폭 가속**시킵니다.

---

## 🔍 왜 음성 처리에 CUDA가 필요한가?

| 작업 종류 | 병목 요소 | CUDA로 개선되는 점 |
|-----------|-----------|--------------------|
| 음성 인식 (ASR) | 딥러닝 모델 추론 (RNN, Transformer 등) | 병렬 연산으로 모델 추론 속도 향상 |
| 음성 합성 (TTS) | 멜스펙트로그램 → 음성 변환 | FastSpeech, HiFi-GAN 등 GPU로 빠르게 처리 |
| 특징 추출 (Feature Extraction) | MFCC, Mel Filter Bank 계산 | NumPy 대비 수십 배 빠른 처리 |
| 실시간 처리 | 짧은 시간 내 처리 필요 | GPU 가속으로 latency 감소 |

---

## ⚙️ CUDA 사용 환경 설정

### 1. CUDA Toolkit 설치
- [NVIDIA CUDA 다운로드](https://developer.nvidia.com/cuda-downloads)
- Python에서 PyTorch 또는 TensorFlow 설치 시 자동으로 GPU 지원 포함 가능

### 2. 드라이버 및 라이브러리
- NVIDIA 드라이버 + cuDNN 설치 권장
- `nvidia-smi`로 GPU 인식 여부 확인

---

## 📦 딥러닝 기반 음성 처리에서 CUDA 사용 예

### PyTorch 기반 음성 인식 예시 (Whisper)

```python
import torch
from transformers import WhisperProcessor, WhisperForConditionalGeneration

# GPU에서 모델 실행
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

model = WhisperForConditionalGeneration.from_pretrained("openai/whisper-small").to(device)
processor = WhisperProcessor.from_pretrained("openai/whisper-small")

# 오디오 입력 전처리 및 인퍼런스
input_features = processor(audio, return_tensors="pt").input_features.to(device)
predicted_ids = model.generate(input_features)

