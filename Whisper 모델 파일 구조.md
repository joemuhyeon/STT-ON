# 📁 Whisper 파일 구조 설명 (OpenAI 공식)

---
```pgsql
whisper/
├── __init__.py
├── audio.py          🔊 오디오 로딩 및 전처리 (mel spectrogram 변환 등)
├── decoding.py       🧠 디코딩 로직 (beam search, sampling 등)
├── model.py          🏗️ Whisper 모델 구조 (Transformer 기반)( model.safetensors(보안) 또는 pytorch_model.bin 중 하나)
├── tokenizer.py      🔤 BPE 토크나이저 처리
├── transcribe.py     📝 전체 음성 전사 파이프라인 구성
├── utils.py          🔧 기타 유틸 함수 모음
├── languages.py      🌐 언어 목록 및 언어 코드 정의
├── timing.py         ⏱️ 디코딩 속도 측정용 도구
```
---
## 🧩 주요 파일 설명

### 🔊 audio.py
- **`load_audio()`**: ffmpeg를 이용해 오디오 파일 로딩 <br>
#ffmpeg - 미디어 파일을 변환하거나 자르거나 합치는 도구
- **`log_mel_spectrogram()`**: 음성을 mel 스펙트로그램으로 변환
- 내부적으로 torchaudio, ffmpeg 사용
➡️ Whisper의 전처리 핵심

### 🧠 decoding.py
- 디코딩 전략 정의:
  - Greedy
  - Beam Search
  - Temperature Sampling
- **`DecodingOptions`**, **`DecodingResult`**, **`decode()`** 함수 제공
- GPU 사용가능(CUDA)
➡️ 음성 → 텍스트 생성의 핵심 모듈 

### 🏗️ model.py
- Transformer 인코더/디코더 구조 정의
- Whisper 클래스 정의 (PyTorch 기반)
- 모델 로딩: **`Whisper.load_model("small")`** ## small, medium, large 각각의 버전 존재

### 🔤 tokenizer.py
- Byte Pair Encoding(BPE) 기반 토크나이저 구현
- **`get_tokenizer()`**, **`Tokenizer`** 클래스 포함
- 언어별 특수 토큰 처리 포함
➡️ 텍스트 ↔ 토큰 변환 담당

### 📝 transcribe.py
- 전체 음성 파일에 대한 전사 처리 함수: **`transcribe()`**
- 다국어 처리, 자동 언어 감지, 자막 형식(SRT/VTT) 생성 기능 포함
➡️ Whisper 파이프라인 핵심 진입점

### 🌐 languages.py
- ISO 언어 코드 ↔ 언어명 매핑
- 언어 자동 인식 및 사용자 지정 처리 시 사용

### 🔧 utils.py
- 디코딩 과정에서 필요한 보조 함수들 제공
- **`format_timestamp`**, **`compression_ratio`** 등

### ⏱️ timing.py
- 디코딩 시간 측정용
- 벤치마크 측정에 사용

### ▶️ cli.py
- CLI로 whisper 실행 가능하게 해줌
- 예 :
  ```bash
  python cli.py example.mp3 --model small
  ```



