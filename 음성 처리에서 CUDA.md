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

## 🧠 핵심 구조
### 🖥️ CPU vs GPU
| 구분    | CPU         | GPU (CUDA)            |
| ----- | ----------- | --------------------- |
| 코어 수  | 수 개 \~ 수십 개 | 수천 개                  |
| 연산 방식 | 직렬 처리       | 병렬 처리                 |
| 용도    | 일반 논리, OS   | 수치 계산, 딥러닝, 이미지/음성 처리 |

---

## ⚙️ CUDA 실행 흐름
```lua
CPU -----------------------> GPU
 |                            |
 | ① 데이터 준비               |
 |                            |
 | ② 커널 실행 명령 전달       |
 |                            |
 |                            ↓
 |                  ③ GPU에서 병렬 연산
 |                            |
 | ④ 결과 다시 CPU로 복사      |
 ↓                            |
사용자에게 결과 보여줌 <--------|
```
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
#### ✅ (2) CUDA Toolkit 설치
- [https://developer.nvidia.com/cuda-downloads]( https://developer.nvidia.com/cuda-downloads) 에서 설치
- PyTorch에서 사용하려는 CUDA 버전에 맞춰 설치 <br>
  예: PyTorch 2.0 + CUDA 11.8 호환시 <br>
  -> CUDA Toolkit 11.8 설치
- 설치 확인: <br>
```bash
nvcc --version
# CUDA compiler version 표시되어야 함
```
#### ✅ (3) cuDNN 설치
- NVIDIA가 제공하는 딥러닝 연산 전용 고속 라이브러리.
- 딥러닝 모델의 핵심 연산인 합성곱(Convolution), 풀링(Pooling), RNN, normalization 등을
GPU에서 훨씬 빠르고 효율적으로 실행할 수 있게 해줌.
- [https://developer.nvidia.com/cudnn](https://developer.nvidia.com/cudnn) 에서 설치
- 설치는 CUDA 버전에 맞는 cuDNN 버전 다운로드 -> 압축해제 -> CUDA폴더에 덮어쓰기
- 예:
```bash
cp -r cuda/include/* /usr/local/cuda/include/
cp -r cuda/lib64/* /usr/local/cuda/lib64/
```
Windows라면 C:\Program Files\NVIDIA GPU Computing Toolkit 밑에 복사
#### ✅ (4) PyTorch 설치 (CUDA 지원)
- PyTorch 공식: [https://pytorch.org/get-started/locally/](https://pytorch.org/get-started/locally/) 에서 설치
- 예: CUDA 11.8 지원 버전 설치 -> 버전에 맞는 PyTorch를 모를 경우 아래 실행
```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```
- 설치 확인:
```python
import torch
print(torch.cuda.is_available())  # → True
print(torch.cuda.get_device_name(0))  # → GPU 이름 출력
```
## 🔍 문제 해결 체크리스
| 문제                                  | 점검 항목                              |
| ----------------------------------- | ---------------------------------- |
| `torch.cuda.is_available()` → False | 드라이버/Toolkit/버전 불일치, CUDA 경로 설정 오류 |
| `nvcc --version` 안됨                 | CUDA Toolkit PATH 환경변수 등록 필요       |
| GPU 인식 안 됨                          | `nvidia-smi` 확인, 물리적 문제 가능         |

#### ✅ 요약
- 1 - GPU 드라이버 설치 → nvidia-smi 확인
- 2 - CUDA Toolkit + cuDNN 설치
- 3 - PyTorch GPU 버전 설치
- 4 - torch.cuda.is_available() → True 확인
- 5 - 그다음부터는 Whisper, ESPnet, Wav2Vec2 등 GPU로 자동 연산됨
---
## 📦 딥러닝 기반 음성 처리에서 CUDA 사용 예

### PyTorch에서 CUDA 사용 예시
PyTorch는 CUDA를 직접 쓰진 않지만 자동으로 활용합니다.
```python
import torch

# GPU 사용 가능 여부 확인
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

# 텐서 연산 GPU에서 수행
a = torch.randn(1000, 1000, device=device)
b = torch.randn(1000, 1000, device=device)
c = torch.matmul(a, b)  # 이 연산은 CUDA에서 수행됨

print(c)

```
📌 이 연산은 내부적으로 cuBLAS, cuDNN, CUDA 커널을 사용하여 GPU에서 빠르게 실행됩니다.
따로 CUDA 커널을 직접 작성하지 않아도 GPU를 사용하게 됩니다.
