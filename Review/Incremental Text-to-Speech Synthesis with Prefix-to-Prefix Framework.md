## [Incremental Text-to-Speech Synthesis with Prefix-to-Prefix Framework (Mingbo Ma et al)](https://arxiv.org/abs/1911.02750)
  
- EMNLP 2020
- Mingbo Ma, Baigong Zheng, Kaibo Liu, Renjie Zheng, Hairong Liu, Kainan Peng, Kenneth Church, Liang Huang  (Baidu Research)  
- [Demo Page](https://inctts.github.io/)
  
### Summary  
  
- 동시번역을 위한 빠른 음성합성 기법 제안  
- 새로 학습할 필요없이 Inference 단에서 수정하여 사용할 수 있는 파이프라인 제안 (Tacotron2 사용)
- 기존 TTS 시스템  
  
![image](https://user-images.githubusercontent.com/42150335/101376816-6bff4800-38f4-11eb-9dca-1592c05c6759.png)
  
Text2Phoneme → Phoneme2Spectrogram → Spectrogram2Wave 단계를 거침
  
- 위와 같은 Full-sentence TTS는 문장 길이가 길어질수록 latency가 길어지는 고질적인 문제점을 가지고 있음  
- 이러한 문제점 해결을 위해 아래 파이프라인을 제안  
  
![image](https://user-images.githubusercontent.com/42150335/101377884-bf25ca80-38f5-11eb-8098-6f0b206d01f6.png)  
  
- Full-sentence TTS가 아닌, Incremental TTS 방식 제안  
- 먼저 만들어진 오디오를 재생하는 동안 뒷단의 오디오를 만들어나가는 방식  
- 이와 같은 파이프라인이 가능하려면 특정 단위로 쪼개야함 (E.g. Word)  
- 하지만 Word 단위로 TTS를 진행한 후, 오디오를 이어붙이게 되면 굉장히 부자연스러운 음성이 합성됨  
- 이를 극복하기 위해 lookahead-k Policy 제안  
  + t번째 target을 만들때 t+k개의 입력 소스를 통해 생성 (첫 k+1 스텝까지는 wait)    
- 결과적으로 음질이 크게 떨어지지 않으면서도 latency를 줄임 (문장이 길수록 효과가 큼)  
