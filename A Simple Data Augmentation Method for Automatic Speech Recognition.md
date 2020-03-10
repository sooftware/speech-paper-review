# SpecAugment:
## 「A Simple Data Augmentation Method for Automatic Speech Recognition」  Review
  
![title](https://postfiles.pstatic.net/MjAyMDAzMTBfMTgw/MDAxNTgzODQ1NTM5MjI3.U9mG8Tl8fKXJU38N7nlTtTKjnZSrXRxUmEPkL7091xgg.Z_56cPISeZT234kYVSOZFChSH32sURm3NE6FVDJCu0Eg.PNG.sooftware/image.png?type=w773)  
https://arxiv.org/abs/1904.08779  
  
## Abstract
  
모델의 Overfitting을 막기 위해 가장 좋은 방법은 데이터가 많은 것입니다. 하지만 데이터가 뿅! 하고 생기는 것이 아니기 때문에 기존 데이터를 활용하여 새로운 데이터를 만들어내는 Augmentation이라는 기법을 사용합니다. 본 논문에서는 음성인식을 위한 간단한 Data-Augmentation을 제안하고, 이를 SpecAugment라고 명명했습니다. 본 논문은 오디오에서 뽑은 피쳐 벡터 (MFCC or Mel-Spectrogram etc ..) 를 input으로 Time warping, Frequency masking, Time masking 3가지 방법으로 Augmentation을 적용했습니다. 성능 테스트를 위한 모델로는 [「Listen, Attend and Spell」](https://github.com/sh951011/Paper-Review/blob/master/Listen%2C%20Attend%20and%20Spell.md) (LAS) 모델을 사용했으며, Language Model과의 **Shallow Fusion**을 통해 인식률 개선을 이뤄냈다고 밝히고 있습니다. 본 논문의 모델은 [LibriSpeech 960h](http://www.openslr.org/12/) 데이터셋과 [Swichboard 300h](https://catalog.ldc.upenn.edu/LDC97S62) 데이터셋에서 **State-Of-The-Art (SOTA)** 를 달성했습니다. 달성한 결과는 아래 표에 정리했습니다.    
  

|Method|LibriSpeech 960h|LibriSpeech 960h|Swichboard 300h|Swichboard 300h|    
|:--:|:--:|:--:|:--:|:--:|    
|          |No LM|With LM|No LM|With LM|  
|Previous         |-|7.5|-|8.3 / 17.3|   
|**LAS + SpecAugment**|6.8|5.8|7.2 / 14.6|6.8 / 14.1|  
  
  
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
  
#

## Introduction
   
딥러닝은 음성인식 분야에 성공적으로 적용이 되었습니다. 하지만, 음성 인식 분야의 연구는 대부분 모델에 초점이 맞춰져서 진행이 되었는데, 본 논문은 이러한 모델들은 쉽게 Overfitting 현상이 발생하며, 많은 양의 데이터를 필요로 한다고 지적하고 있습니다.  
  

### Traditional Data-Augmentation for Audio
  
그리고 본 논문은 기존의 Augmentation이 어떤 방식으로 적용되었었는지에 대한 설명을 간략하게 합니다.  
  
#### Noise injection  
  
![noise-ingection](https://postfiles.pstatic.net/MjAyMDAzMTFfMTky/MDAxNTgzODYyMTgxNjEz.4-taA67o4zYethS2nkXI7mmgsWVFpBTWGsFSB4eDTNsg.E0EYGEG6zzK9zJ4n7pXLrVu1zYD5ZnGnU14b4NQtnOcg.PNG.sooftware/image.png?type=w773)  
  
기존 데이터에 임의의 난수를 더하여 Noise를 추가해주는 방법입니다.  
  
#### Shifting Time  
  
![shiftting-time](https://postfiles.pstatic.net/MjAyMDAzMTFfODYg/MDAxNTgzODYyMjA2ODU3.cdo4B6N7B_3ut6Cg-fB2XhKnXRyM7t_inYtCJ_11PYQg.LRzvVgjn3bKR-maieujxTC-XF5BVTNb8LdZcJzamkqQg.PNG.sooftware/image.png?type=w773)  
  
임의의 값만큼 음성 신호를 좌/우로 shift하고 빈 공간은 0으로 채우는 방법입니다.  
  
#### Changing Pitch
  
![changing-pitch](https://postfiles.pstatic.net/MjAyMDAzMTFfMjI3/MDAxNTgzODYyMjI2Mzk2.ebxn9cuq8oDWMfWZTaDH-oncrBjRr4A-SWVYB9ozbtQg.OtYDyy_sMrgTgDl3-6b-_TW61Nq80NEYzPfdEGf6oR4g.PNG.sooftware/image.png?type=w773)    
  
기존 음성 신호의 Pitch(음높이, 주파수)를 랜덤하게 변경해주는 방법입니다.  
  
#### Changing Speed
  
![changing-speed](https://postfiles.pstatic.net/MjAyMDAzMTFfMTEg/MDAxNTgzODYyMjQ0ODU3.3UCMz-mY72XLLtQOuKn5_RmR_W7aB2o827b73Qa1i20g.ltl5l-7WVHOba5HsxSuU1QXjJ2Pcoyymh4blItMZb5Ig.PNG.sooftware/image.png?type=w773)

기존 음성 신호의 속도를 빠르게 / 느리게 바꿔주는 방법입니다.  

기존 음성 신호에 대한 Augmentation은 위와 같이 raw audio를 변형하는 방법들이었습니다.  
하지만 본 논문에서는 이와 같이 주장합니다.  
  
```
어차피 사용하는 피쳐는 MFCC / log mel spectrogram인데, 이쪽을 변형하는게 쉽고 빠르지 않아?"
```  
  
또한 이러한 방법을 이와 같이 표현합니다.  
```
This method is simple and computationally cheap to apply.
```  

log mel spectrogram을 이미지처럼 다루는 겁니다. 이렇게 계산 비용이 적게 들기 때문에 학습을 하면서 바로바로 Augmentation을 적용할 수 있었다고 합니다. SpecAugment는 앞에서 언급했듯이 3가지 종류의 변형을 적용했습니다.  
  
1.  Time Warping  
2.  Time Masking  
3.  Frequency Masking  
  
## Augmentation Policy
  
