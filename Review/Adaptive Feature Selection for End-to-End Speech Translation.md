## [Adaptive Feature Selection for End-to-End Speech Translation (Biao Zhang et al)](https://arxiv.org/abs/2010.08518)
  
- EMNLP 2020  
- Biao Zhang, Ivan Titov, Barry Haddow, Rico Sennrich

### Summary
  
- End-to-End Speech Translation (E2E ST)를 다룬 논문  
- Speech Translation
  + Cascade: 음성 (source) → 음성인식 모델 → 텍스트 (source) → 번역 모델 → 텍스트 (target)
  + E2E: 음성 (source) → 음성번역 모델 → 텍스트 (target)  
- Cascade 방식은 음성인식에서의 오류가 기계번역으로 전파가 되는 단점이 있음
- E2E 번역이 최근 많이 연구되고 있으나, Cascade 방식의 성능을 따라잡지 못하고 있음   
  
![image](https://user-images.githubusercontent.com/42150335/101368190-32294400-38ea-11eb-924b-5b0a2e25d2e6.png)

- E2E ST가 어려운 주된 이유로, 음성마다 단어 발화 길이가 다르며, 노이즈 혹은 중간중간 끊기는 등 일관적이지 않다는 특징 때문이라고 주장  
- 그래서 인코딩 된 피쳐를 선택적으로 사용해야 된다고 주장 (Adaptive Feature Selection)      
- AFS는 인코더 아웃풋에서 필요없는 프레임은 제거하는 역할을 함 (L<sub>0</sub>Drop - Zhang et al., 2020)
- 결과적으로 본 논문은 아래와 같은 파이프라인을 제안함
  
<img src="https://user-images.githubusercontent.com/42150335/101366218-073df080-38e8-11eb-8699-dd6ebc2d70dc.png" width=300>  
  
- Training Pipeline
  1. ASR 모델 학습 (Hybrid Cross Entropy + CTC)  
  2. AFS 모델을 추가해서 ASR 모델 파인튜닝  
  3. ASR & AFS 모델은 Freeze한 채로 ST Encoder, ST Decoder 학습  
- Result on MuST-C En-De  
  
<img src="https://user-images.githubusercontent.com/42150335/101370007-4a9a5e00-38ec-11eb-8f41-7f6de1b9d583.png" width=500>
  
  + AFS는 모델을 더 빠르게 하면서도 성능을 높였음
  + 성능은 Cascade보다는 살짝 낮음
