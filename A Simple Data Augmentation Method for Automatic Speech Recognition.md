# SpecAugment:
## 「A Simple Data Augmentation Method for Automatic Speech Recognition」  Review
  
![title](https://postfiles.pstatic.net/MjAyMDAzMTBfMTgw/MDAxNTgzODQ1NTM5MjI3.U9mG8Tl8fKXJU38N7nlTtTKjnZSrXRxUmEPkL7091xgg.Z_56cPISeZT234kYVSOZFChSH32sURm3NE6FVDJCu0Eg.PNG.sooftware/image.png?type=w773)  
https://arxiv.org/abs/1904.08779  
  
## Abstract
  
모델의 Overfitting을 막기 위해 가장 좋은 방법은 데이터가 많은 것입니다. 하지만 데이터가 뿅! 하고 생기는 것이 아니기 때문에 기존 데이터를 활용하여 새로운 데이터를 만들어내는 Augmentation이라는 기법을 사용합니다. 본 논문에서는 음성인식을 위한 간단한 Data-Augmentation을 제안하고, 이를 SpecAugment라고 명명했습니다. 본 논문은 오디오에서 뽑은 피쳐 벡터 (MFCC or Mel-Spectrogram etc ..) 를 input으로 Time warping, Frequency masking, Time masking 3가지 방법으로 Augmentation을 적용했습니다. 성능 테스트를 위한 모델로는 [「Listen, Attend and Spell」](https://github.com/sh951011/Paper-Review/blob/master/Listen%2C%20Attend%20and%20Spell.md) (LAS) 모델을 사용했으며, Language Model과의 **Shallow Fusion**을 통해 인식률 개선을 이뤄냈다고 밝히고 있습니다. 본 논문의 모델은 [LibriSpeech 960h](http://www.openslr.org/12/) 데이터셋과 [Swichboard 300h](https://catalog.ldc.upenn.edu/LDC97S62) 데이터셋에서 **State-Of-The-Art (SOTA)** 를 달성했습니다.  
  
### Data Augmentation  
  
자세히 들어가기 앞서, Data-Augmentation이 뭔지 부터 살펴봅시다.  
  
![Augmentation](https://postfiles.pstatic.net/MjAyMDAzMTBfMzYg/MDAxNTgzODQ2NjA2MzUy.B4mA43yYLqG_oUSRy1djtBTGUYAI1X4GUFScWfkKsmog.g0SLMSyoMnfneosZJyvJbDiVj7AjiosFxwvs6QRGMdAg.PNG.sooftware/image.png?type=w773)
  
Augmentation이란, 데이터를 부풀려서 모델의 성능을 향상시키는 기법입니다.  
이미지 인식 분야에서 많이 쓰이는 방법으로, 좌우 반전, 사진의 일부 발췌, 밝기 조절 등을 적용하여 한정된 데이터를 조금씩 변형시켜 새로운 데이터처럼 활용하는 방법입니다.  
  
### Augmentation을 하는 이유
  
1. Preprocessing 및 .Augmentation을 하면 대부분의 경우 성능이 향상된다.  
2. 원본 데이터를 활용하여 추가하는 개념이므로 성능이 저하될 염려가 없다.  
3. 방법이 간단하며 패턴이 정해져 있다.  
  
단기간에 성능 향상을 원한다면, Ensemble, Augmentation을 활용하라는 말이 있을 정도로 그 효과가 검증됐다고 합니다.  
저번 네이버 해커톤 - Speech 대회 참여 당시에도, 상위권 팀들은 Ensemble, Augmentation을 거의 모두 적용했었습니다. 또한 Augmentation을 적용하는 방법은 매우 다양하기 때문에, 여러 방법도 적용이 가능하다는 장점이 있습니다.  
  
## Introduction
   
딥러닝은 음성인식 분야에 성공적으로 적용이 되었습니다. 하지만, 음성 인식 분야의 연구는 대부분 모델에 초점이 맞춰져서 진행이 되었는데, 본 논문은 이러한 모델들은 쉽게 Overfitting 현상이 발생하며, 많은 양의 데이터를 필요로 한다고 지적하고 있습니다.  

  
  

  


