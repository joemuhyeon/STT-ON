# STT-ON
음성 인식 AI 

## ✅ANS(Automatic Speech Recognition)
- 자동 음성 인식(Automatic Speech Recognition)은 음성 신호를 입력으로 받아들여 텍스트로 변환하는 기술이다. 음성 인식 엔진을 사용하여
 음성 신호를 분석하고 인간의 음성을 텍스트로 해석하는 과정을 수행한다.
### 1. 푸리에 변환(Fourier transform)
- 자동 음성 인식(Automatic Speech Recognition)의 첫 번째 단계는 음성 신호의 특징 추출이다. 주로 푸리에 변환(Fourier transform)을 사용하여 음성 신호를 주파수 영역으로 변환한 후, 주파수 스펙트럼에서 특징적인 정보를 추출한다.
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9967FA3359B63D8122" alt="이미지" width="400" height="270"/>
그림 1. 푸리에 변환 (그림출처: 위키피디아)

#### 1-1 쉬운설명
- 복잡한 소리를 여러 개의 단순한 소리로 쪼개는 방법
- 노래에 드럼, 피아노, 기타, 사람 목소리 같은 여러 소리가 섞여있음<br>
  -> 피아노 소리, 드럼소리, 기타소리, 사람목소리 따로 따로 분리해줌

#### 1-1 쓰는이유
- 사람이 들을 때는 여러 소리가 한꺼번에 들리지만, 컴퓨터는 각각의 소리가 어떻게 생겼는지 알아야 더 잘 이해할 수 있음.<br>
 -> 소리를 분리하면, 컴퓨터가 이 소리를 분석하고 처리하기 쉬워짐.
- 어느 부분에 노이즈가 있는지 어디를 강화해야 할지 판단할 수 있음.

#### 1-2 푸리에 변환(Fourier transform)방법
&nbsp;&nbsp; ### 1-2-1 🎤 예시 상황:
-어떤 사람이 "안녕하세요" 라고 1초 동안 말했을때
### 2. 특징 추출 (Feature Extraction)
- 푸리에 변환(Fourier transform) 결과를 바탕으로 멜 주파수 켑스트럼 계수(MFCC) 나 멜 스펙트로그램 같은 음성 특징 벡터를 만든다.
- 
