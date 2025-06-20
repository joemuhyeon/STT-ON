# 📁 Whisper 파일 구조 설명 (OpenAI 공식)

---
```pgsql
whisper/
├── __init__.py
├── audio.py          🔊 오디오 로딩 및 전처리 (mel spectrogram 변환 등)
├── decoding.py       🧠 디코딩 로직 (beam search, sampling 등)
├── model.py          🏗️ Whisper 모델 구조 (Transformer 기반)
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
- log_mel_spectrogram(): 음성을 mel 스펙트로그램으로 변환
- 내부적으로 torchaudio, ffmpeg 사용
➡️ Whisper의 전처리 핵심

### 🧠 decoding.py
- 디코딩 전략 정의:
  - Greedy
  - Beam Search
  - Temperature Sampling
- DecodingOptions, DecodingResult, decode() 함수 제공
- GPU 사용가능(CUDA)
➡️ 음성 → 텍스트 생성의 핵심 모듈 
