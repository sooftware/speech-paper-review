# Deep Speech: Scaling up end-to-end speech recognition  
  
![title](https://postfiles.pstatic.net/MjAyMDAyMjNfMTQ1/MDAxNTgyMzkwNTAyMzI5.qYtgph7nxA4sOZlHd8-dw9dOmXeEZvz3zifBjyMYNaUg.uX_2ZheLYRPxPHJogipB50IrpYX7yYi5jNPWbWGv2sog.PNG.sooftware/image.png?type=w773)  
  
https://arxiv.org/pdf/1412.5567.pdf (Awni Hannun et al. 2014)  
  
## Abstract  
  
 본 논문은 2014년도에 나온 논문이다. 논문을 읽어본 결과, 당시에는 음성인식에 End-to-End 방식의 딥러닝을 적용한 사례가 없던 모양이다. (또는 주목할만한 성과가 나오지 않았던 모양이다.) 본 논문에서는 End-to-End 방식으로 Switchboard Hub5'00 데이터셋에서 16.0%의 Error Rate를 기록하며 **State-Of-The-Art** (SOTA) 를 달성한 성과를 밝히고 있다. 기존 음성인식의 traditional한 방식은 전처리 과정이 상당히 많이 필요했지만, 이러한 과정 없이 데이터와 레이블만을 이용한 End-to-End 방식으로 이러한 성과를 냈음을 거듭 강조하고 있다. 그리고 이전 방식으로는 노이즈가 있는 환경에서 급격히 떨어졌는데 반하여, 본 논문 방식으로는 노이즈가 있는 환경에서도 좋은 성능을 기록했다고 한다. 즉, 기존 방식보다 더 간단하면서도 좋은 성능을 기록한 End-to-End 방식의 Speech-Recognition 모델을 소개하는 논문이다.  

## Introduction

Abstract에서 강조한 내용을 다시 한번 강조한다. 기존 traditional한 방식은 전문가들의 손이 많이 가야했다. (노이즈 필터링 등..) 하지만 그러한 노력에도 불구하고, 실제 노이즈가 낀 상황에서의 인식률은 좋지 못했다. 하지만 End-to-End 방식으로 이러한 2가지의 단점을 개선할 수 있다고 주장한다.   
  
 물론 End-to-End 방식으로 가기 위해서는 몇가지 고려해야할 사항들이 있었지만, 본 논문에서는 기존 연구 결과들을 참고하여 End-to-End 방식을 시도할 수 있었다고 말한다. 그리고, 본 논문에서는 RNN 모델을 사용했다. 뒤에 더 자세히 설명하겠지만 본 논문에서는 학습 시간을 단축시키기 위해 많은 고려를 한 것으로 보인다.  
   
## RNN Training Setup
  
