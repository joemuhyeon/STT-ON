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

## ⚙️ CUDA 사용 환경 설정 (PyTorch + 음성처리용)

음성 인식(ASR), 음성 합성(TTS) 같은 모델들은 대체로 **딥러닝 기반**이며  
**GPU(CUDA)** 없이는 **학습 및 추론 속도가 매우 느립니다**.

이 섹션에서는 **CUDA를 제대로 활용하기 위한 환경 설정 방법**을 안내합니다.

---

### 🧩 1. 시스템 요구 사항

| 구성 요소 | 최소 사양 | 권장 사양 |
|------------|------------|------------|
| GPU | NVIDIA GPU (예: GTX 1060 이상) | RTX 30xx 또는 A6000 등 |
| 운영체제 | Windows 10 / Ubuntu 20.04 | Ubuntu 권장 |
| RAM | 8GB 이상 | 16GB 이상 |
| 저장공간 | 10GB 이상 여유 | SSD 권장 |

---

### 🧱 2. 필수 소프트웨어

| 소프트웨어 | 설명 |
|------------|------|
| NVIDIA GPU Driver | 그래픽카드에 맞는 최신 드라이버 |
| CUDA Toolkit | GPU에서 실행 가능한 연산을 위한 핵심 라이브러리 |
| cuDNN | 딥러닝 연산 최적화를 위한 NVIDIA의 고성능 라이브러리 |
| Python | 보통 3.8~3.10 버전 권장 |
| PyTorch (GPU 버전) | CUDA 기반 연산을 자동으로 처리 |

---

### 🔧 3. 설치 절차 (Windows / Ubuntu)

#### ✅ (1) NVIDIA 드라이버 설치

- [https://www.nvidia.com/Download/index.aspx](https://www.nvidia.com/Download/index.aspx) 에서 설치
- 설치 후 **`nvidia-smi`** 명령어로 정상 설치 확인

```bash
nvidia-smi
# → GPU 이름, 드라이버 버전, 메모리 사용량 등이 출력되어야 함
```
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
```
