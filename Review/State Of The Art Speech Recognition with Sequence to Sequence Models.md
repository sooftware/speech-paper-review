# 「STATE-OF-THE-ART SPEECH RECOGNITION WITH SEQUENCE-TO-SEQUENCE MODEL」 Review
  
![title](https://postfiles.pstatic.net/MjAyMDAzMjRfNjEg/MDAxNTg1MDI5MjM0NzE4.Erz3moRU6RYrvzJltHM-pZ8VS454S_ix0MMob30IT9Ig.0wAmtiJGW_QIIqWabuAESuw0B-kJCGa4C6Mvb7vQPVQg.PNG.sooftware/image.png?type=w773)  
https://arxiv.org/abs/1712.01769  
  
본 논문은 제가 진행하는 [프로젝트](https://github.com/sh951011/Korean-Speech-Recognition)의 Contributor 분께서 추천해주신 논문으로, 본 논문에서 적용한 Multi-Head Attention을 적용하여 인식률이 향상되었습니다. 또한 본 논문에서는 Word-Piece를 사용하지만, 한국어에서는 Word-Piece 적용시 성능이 저하된다고 합니다. [Show Issue](https://github.com/sh951011/Korean-Speech-Recognition/pull/9)

## Abstract
  
논문 이름에서부터 밝히듯이, 500h Voice Search 분야에서 **State-Of-The-Art (SOTA)** 를 달성한 논문입니다. 어텐션 기반의 Seq2seq구조인 Listen, Attend and Spell (LAS) 아키텍쳐를 사용했다고 합니다. LAS 구조는 기존의 음향 모델, 발음 모델, 언어 모델로 구성된 방식에서 하나의 Neural Network로 End-to-End 학습을 가능하게한 구조입니다. ([「Listen, Attend and Spell」 Paper Review](https://github.com/sh951011/Paper-Review/blob/master/Review/Listen%2C%20Attend%20and%20Spell.md)) 본 논문에서는 grapheme (문자소) 모델이 아닌 word-piece 모델을 사용했으며, Multi-Head Attention을 도입했다고 합니다. 그 외에도 최적화를 위해 Synchronous training, scheduled sampling, label smoothing 등을 사용했다고 밝힙니다. 특이한 점으로 인코더 부분에 Bidirectional-LSTM이 아닌 Unidirectional-LSTM을 사용했다고 합니다.  
  
## Introduction
  
Sequence-to-Sequence 모델은 Autonomic Speech Recognition (ASR) Task에서 탁월한 성능을 보여주었습니다. 이 글을 쓰는 지금 2020년에도 아직까지 관련 논문들과 SOTA를 Sequence-to-Sequence 모델이 점유하고 있습니다. Neural Machine Translation 분야는 Seq2seq 보다는 Transformer 모델이 더 빠르고 좋은 성능을 내는 듯 합니다만, Speech 분야에서는 Transformer 모델이 다소 부진한 듯 합니다. (NMT에서의 압도적인 성능에 비해서입니다 ㅎㅎ..) 제가 네이버 AI 해커톤 참여 당시, 멘토분께서 Transformer는 데이터가 적을 때 성능이 그렇게 좋지는 않다고 하셨습니다. 아마 데이터가 적은 음성 분야라 더 두드러지는 특징이 아닐까 싶습니다. 실제로 네이버 대회 당시 100시간이라는 한정된 데이터로 진행을 하다보니, Transformer를 사용한 팀들이 어텐션 기반의 Seq2seq 모델을 사용한 팀들에게 밀리는 현상이 있었습니다. 본 논문도 Transformer보다 뒤에 나온 논문이지만, Transformer가 아닌 Seq2seq 기반으로 모델을 구성한 것을 볼 수 있습니다. 단, Transformer를 제안한 「Attention Is All You Need」 논문에서 나온 **Multi-Head Attention**을 사용했습니다. 또한 뒤에서 다룰 **Word-Piece Model (WPM)**, **Scheduled Sampling (SS)**, **label smoothing**, **Asynchronous SGD**, **language model** 등을 사용했습니다. 자세한 내용은 뒤에서 다루겠습니다.

 