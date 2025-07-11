# STT-ON
음성 인식 AI 

## ✅ANS(Automatic Speech Recognition)
- 자동 음성 인식(Automatic Speech Recognition)은 음성 신호를 입력으로 받아들여 텍스트로 변환하는 기술이다. 음성 인식 엔진을 사용하여
 음성 신호를 분석하고 인간의 음성을 텍스트로 해석하는 과정을 수행한다.

# 📘1. 푸리에 변환(Fourier transform)
- 자동 음성 인식(Automatic Speech Recognition)의 첫 번째 단계는 음성 신호의 특징 추출이다. 주로 푸리에 변환(Fourier transform)을 사용하여 음성 신호를 주파수 영역으로 변환한 후, 주파수 스펙트럼에서 특징적인 정보를 추출한다.
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9967FA3359B63D8122" alt="이미지" width="400" height="270"/>
그림 1. 푸리에 변환 (그림출처: 위키피디아)

#### 🤔1-1 쉬운설명
- 복잡한 소리를 여러 개의 단순한 소리로 쪼개는 방법
- 노래에 드럼, 피아노, 기타, 사람 목소리 같은 여러 소리가 섞여있음<br>
  -> 피아노 소리, 드럼소리, 기타소리, 사람목소리 따로 따로 분리해줌

#### 🤔1-1 쓰는이유
- 사람이 들을 때는 여러 소리가 한꺼번에 들리지만, 컴퓨터는 각각의 소리가 어떻게 생겼는지 알아야 더 잘 이해할 수 있음.<br>
 -> 소리를 분리하면, 컴퓨터가 이 소리를 분석하고 처리하기 쉬워짐.
- 어느 부분에 노이즈가 있는지 어디를 강화해야 할지 판단할 수 있음.

### 1-2📘푸리에 변환(Fourier transform)방법

#### 1-2-1 🎤 예시 상황:<br>
- 어떤 사람이 "안녕하세요" 라고 1초 동안 말했을때

#### 1-2-2 ✅1단계: 소리를 짧게 자른다(프레임 분할)
- 원래 음성은 1초 동안 쭉 이어진 파형
- 이걸 0.025(25ms)씩 잘라서 작은 조각으로 나눔<br>
  ->1초 = 1000ms이니까, 약 40개의 조각이 생김.
  📦 예시:
"안녕하세요" → [📦][📦][📦]...[📦] (총 40개 조각)

#### 1-2-2 ✅2단계: 각 조각을 푸리에 변환한다(주파수 분석)
- 각 조각마다 "이 안에 어떤 소리가 들어 있나?" 분석함.
- 푸리에 변환을 하면: <br>
📦 조각 1: 저음 70%, 고음 30% <br>
📦 조각 2: 저음 40%, 중음 40%, 고음 20% <br>
📦 조각 3: 고음 80%, 나머지 20% ... <br>
각 조각의 '주파수 성분(음 높낮이 비율)'을 알 수 있게 됌.

#### 1-2-2 ✅3단계: 표로 정리한다(스펙트로그램)
- 각 조각의 주파수 성분을 표처럼 쭉 이어 붙임.
- 가로축 : 시간(조각 번호) /  세로축: 주파수 (소리의 높이) / 색깔 : 세기(강한 소리는 진한색) <br>
🟪🟪⬛⬛⬛⬜⬜⬜⬜ <br>
⬛⬛🟪🟪🟨⬜⬜⬜⬜ <br>
→ 이런 식의 그림이 나옴 (이걸 스펙트로그램이라 부름)
## ✨핵심
- 음성 인식 모델은 "파형"이 아닌 "스펙트로그램"을 입력으로 사용.
- 즉, 푸리에 변환은 소리를 AI가 이해할 수 있는 데이터로 바꾸는 핵심 과정.
## 📚 문서
- [음향 특징 추출](음향특징추출.md)
