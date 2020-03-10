# 「A Structured Self-attentive Sentence Embedding」  Review  
  
![title](https://postfiles.pstatic.net/MjAyMDAzMTBfMTA2/MDAxNTgzNzgyMzYwODA1.ZhM8YAx4iOCzc02mlKFRmXWVXeGbn11y9ww1yPLdLowg.b2hy83NDDdNMloBZxrBbTInpGGtkFuyvNlVZ3mqwoBYg.PNG.sooftware/image.png?type=w773)  
https://arxiv.org/abs/1703.03130  
  
## Introduction  
  
Bi-LSTM과 Self-Attention을 이용해서 문장 벡터 (Sentence Embedding)을 구하는 논문입니다.  
ICLR 2017에 기재된 논문입니다.  
  
당시에도 Bi-LSTM 같은 경우는 워낙 많이 쓰이는 구조이기 때문에, 제가 관심있었던 부분인 Self-Attention에 초점을 맞추겠습니다.  
  
어텐션은 그 성능이 입증된만큼 다양한 버젼으로 존재합니다.  
  
![attention-score-function](https://postfiles.pstatic.net/MjAyMDAzMTBfMjcw/MDAxNTgzNzgyNTYzOTQy.wY-XZqY1i_Ndp2ISwMGqcu0mIwID61_zhbDeaxWE2T8g.2M6c4feJUFmS0PF4ljNmc3vBaVRvF47YRhEcQvE0ITkg.PNG.sooftware/image.png?type=w773)  
출처 : https://lilianweng.github.io/lil-log/2018/06/24/attention-attention.html
  
위의 표와 같이 다양한 버젼의 어텐션이 존재합니다.  
어떤 문제냐, 어떤 환경에서 사용할 것인가 등에 의해 많은 변형이 있습니다.  
  
본 논문은 이러한 여러 스코어 함수 중 Self-Attention을 사용해서 Sentence Embedding을 진행하고, 그 결과를 기재한 논문입니다.  
  
Self-Attention 같은 경우는 이 [논문](https://arxiv.org/pdf/1601.06733.pdf)에서 제안됐다고 합니다.  
  
## Self-Attention  
  
Intra-Attention이라고도 불립니다.  
Self-Attention은 한 단어가 한 문장 안에서 어디에 집중하는지를 계산합니다.  
유명한 「Attention Is All You Need」 논문에서 사용되어서 많이들 알고 계실 겁니다.  
하지만, Transformer에서 사용한 방식과는 디테일이 조금 다릅니다.  
Transformer에서는 Multi-Head Attention, Scaled-Dot 등의 개념이 결합되었습니다.  
하지만, 자기 자신의 Sequence에 집중한다는 전체적인 맥락은 비슷합니다.  
  
### Formula
  
Self-Attention의 수식은 간단합니다.  
  

<img src="https://postfiles.pstatic.net/MjAyMDAzMTBfMTU5/MDAxNTgzNzkzMjUwNDk2.wlO1eB5jN1tuYW4gbXGkSchwaY0mcwimcGBYqwNoix4g.a29JuOtcOqjr6iHNDubN5ZdxPNF1hMwZExfKnVnZVukg.PNG.sooftware/image.png?type=w773">  
  
Bi-LSTM에서 나온 H와 weight를 행렬곱을 하고 (여기서 weight는 학습되는 벡터입니다.)  tanh를 이용하여 [-1, 1]의 범위로 맞춰줍니다.  
  
그리고 여기에 벡터 W를 곱합니다. 이 벡터 역시 학습이 필요한 벡터입니다.  
  
그리고 이 결과를 softmax를 취해줌으로써 Attention-Score를 구하게 됩니다.  
  
복잡해보이지만, 사실 중간에 tanh가 끼어있는 것을 제외하고는, 레이어 2개의 Multi-Layer Perceptron (MLP) 를 적용한 것입니다.  
  
그리고 그 값을 Softmax로 점수화 해준 것이고요.
  
여기서, 필요한 것은 Bi-LSTM에서 나온 자신의 시퀀스와 학습이 필요한 2개의 벡터밖에 업습니다.  
  
t시점의 디코더 아웃풋 (Q) 이 필요한 다른 어텐션과는 대비되는 차이점입니다.  
Self-Attention을 Q, K, V가 모두 동일한 어텐션이라고 설명하는 글도 봤습니다.  
  
그래서 본 논문에서는 이러한 특징을 가지는 Self-Attention을 이용해서 
Sentence-Embedding을 했다고 합니다.  
  
저는 본 논문의 Self-Attention에만 관심이 있었기 때문에, 어떤 결과가 나왔는지에 대해서는 읽어보지 않았습니다.
  

  

