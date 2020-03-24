# 「STATE-OF-THE-ART SPEECH RECOGNITION WITH SEQUENCE-TO-SEQUENCE MODEL」 Review
  
![title](https://postfiles.pstatic.net/MjAyMDAzMjRfNjEg/MDAxNTg1MDI5MjM0NzE4.Erz3moRU6RYrvzJltHM-pZ8VS454S_ix0MMob30IT9Ig.0wAmtiJGW_QIIqWabuAESuw0B-kJCGa4C6Mvb7vQPVQg.PNG.sooftware/image.png?type=w773)  
https://arxiv.org/abs/1712.01769  
  
본 논문은 제가 진행하는 [프로젝트](https://github.com/sh951011/Korean-Speech-Recognition)의 Contributor 분께서 추천해주신 논문으로, 본 논문에서 적용한 Multi-Head Attention을 적용하여 인식률이 향상되었습니다. 또한 본 논문에서는 Word-Piece를 사용하지만, 한국어에서는 Word-Piece 적용시 성능이 저하된다고 합니다. [Show Issue](https://github.com/sh951011/Korean-Speech-Recognition/pull/9)

## Abstract
  
논문 이름에서부터 밝히듯이, 500h Voice Search 분야에서 **State-Of-The-Art (SOTA)** 를 달성한 논문입니다. 어텐션 기반의 Seq2seq구조인 Listen, Attend and Spell (LAS) 아키텍쳐를 사용했다고 합니다. LAS 구조는 기존의 음향 모델, 발음 모델, 언어 모델로 구성된 방식에서 하나의 Neural Network로 End-to-End 학습을 가능하게한 구조입니다. ([「Listen, Attend and Spell」 Paper Review](https://github.com/sh951011/Paper-Review/blob/master/Review/Listen%2C%20Attend%20and%20Spell.md)) 본 논문에서는 grapheme (문자소) 모델이 아닌 word-piece 모델을 사용했으며, Multi-Head Attention을 도입했다고 합니다. 그 외에도 최적화를 위해 Synchronous training, scheduled sampling, label smoothing 등을 사용했다고 밝힙니다. 특이한 점으로 인코더 부분에 Bidirectional-LSTM이 아닌 Unidirectional-LSTM을 사용했다고 합니다.  
  
## Introduction
  
