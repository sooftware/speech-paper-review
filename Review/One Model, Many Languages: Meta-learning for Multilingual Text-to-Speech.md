# One Model, Many Languages: Meta-learning for Multilingual Text-to-Speech  
  
Tomáš Nekvinda, Ondřej Dušek  
Charles University  
INTERSPEECH, 2020  
  
## Reference
  
* [ArXiv](https://arxiv.org/abs/2008.00768)  
* [Source Code](https://github.com/Tomiinek/Multilingual_Text_to_Speech)  
* [Demo Webpage](https://tomiinek.github.io/multilingual_speech_samples/)  
* [Tacotron](https://arxiv.org/abs/1703.10135), [Tacotron2](https://arxiv.org/abs/1712.05884) 
* [CSS 10](https://github.com/Kyubyong/css10)  
* [Common Voice](https://commonvoice.mozilla.org/en/datasets) 
  
## Summary
  
* Multilingual Speech Synthesis  
* Voice Cloning  
* Code switching  
* Tacotron2 base architecture
  
## Abstract
  
## Tacotron
  
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwnGyQ%2FbtqDblNauXg%2FJsSXkwgQY1yc3lIHtdgIP0%2Fimg.png" width=700>

* 딥러닝 기반 음성합성의 대표적인 모델  
* Attention + Sequence-to-Sequence의 TTS 버전  
* Griffin-Lim Vocoder 사용  


## Tacotron2  
  
<img src="https://user-images.githubusercontent.com/42150335/94840259-1cfbe900-0453-11eb-8803-cac2ea30b425.png" width=470>  
  
* Mel-Prediction Network : Attention based Sequence-to-Sequence Network  
  + 인코더에서 Bi-directional LSTM 적용
  + Location Sensitive Attention 적용 (음성 Alignment에 강한 어텐션)
  + 인코더, 디코더에 Convolution Layer 적용
* Vocoder : WaveNet  
  + 장점 : 상당히 고품질의 음성으로 변환
  + 단점 : 엄청나게 느림
  
  
## Model Architecture
  
<img src="https://github.com/Tomiinek/Multilingual_Text_to_Speech/raw/master/_img/generated.png" width=800>
  
### This Paper`s Model: Generated (Gen)  
  
### Baselines: Shared, Separate & Single  
  
## Dataset
  
## Experiment  
  
## Conclusion
  
