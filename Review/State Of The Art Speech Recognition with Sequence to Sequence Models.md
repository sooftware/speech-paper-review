# 「STATE-OF-THE-ART SPEECH RECOGNITION WITH SEQUENCE-TO-SEQUENCE MODEL」 Review
  
![title](https://postfiles.pstatic.net/MjAyMDAzMjRfNjEg/MDAxNTg1MDI5MjM0NzE4.Erz3moRU6RYrvzJltHM-pZ8VS454S_ix0MMob30IT9Ig.0wAmtiJGW_QIIqWabuAESuw0B-kJCGa4C6Mvb7vQPVQg.PNG.sooftware/image.png?type=w773)  
https://arxiv.org/abs/1712.01769  
  
본 논문은 제가 진행하는 [프로젝트](https://github.com/sh951011/Korean-Speech-Recognition)의 Contributor 분께서 추천해주신 논문으로, 본 논문에서 적용한 Multi-Head Attention을 적용하여 인식률이 향상되었습니다. 또한 본 논문에서는 Word-Piece를 사용하지만, 한국어에서는 Word-Piece 적용시 성능이 저하된다고 합니다. [Show Issue](https://github.com/sh951011/Korean-Speech-Recognition/pull/9)

## Abstract
  
논문 이름에서부터 밝히듯이, 500h Voice Search 분야에서 **State-Of-The-Art (SOTA)** 를 달성한 논문입니다.  
 어텐션 기반의 Seq2seq구조인 Listen, Attend and Spell (LAS) 아키텍쳐를 사용했습니다. LAS 구조는 이전에 음향 모델, 발음 모델, 언어 모델로 구성된 방식에서 하나의 Neural Network로 End-to-End 학습이 가능한 구조입니다.   
   
 본 논문에서는 grapheme (문자 단위) 모델이 아닌 word-piece (단어 단위) 모델을 사용했으며, Multi-Head Attention을 도입했다고 합니다. 그 외에도 최적화를 위해 Synchronous training, scheduled sampling, label smoothing 등을 사용했다고 밝힙니다.  
   
특이한 점으로 빠른 인식 및 학습을 위해 인코더 부분에 Bidirectional-LSTM이 아닌 Unidirectional-LSTM을 사용했다고 합니다.  
  
## Introduction
  
Sequence-to-Sequence 모델은 Autonomic Speech Recognition (ASR) Task에서 탁월한 성능을 보여주었습니다.   
2015년에 「Listen, Attend and Spell」 논문에서 Seq2seq 아키텍처를 도입한 이후로 이 글을 쓰는 지금 2020년까지도 관련 논문들이 많이 나오고 있고 SOTA 모델에서도  Sequence-to-Sequence 모델이 많이 점유하고 있습니다.  
  
Neural Machine Translation 분야에서 엄청난 성능을 자랑하는 Transformer가 Speech 분야에서는 Transformer 모델이 다소 부진한 듯 합니다. (NMT에서의 압도적인 성능에 비해서입니다 ㅎㅎ..)   
  
제가 네이버 AI 해커톤 참여 당시, 멘토분께서 Transformer는 데이터가 적을 때 성능이 그렇게 좋지 않다고 하셨습니다. 아마 데이터가 적은 음성 분야라 더 두드러지는 특징이 아닐까 싶습니다. 실제로 네이버 대회 당시 100시간이라는 한정된 데이터로 진행을 하다보니, Transformer를 사용한 팀들이 어텐션 기반의 Seq2seq 모델을 사용한 팀들에게 밀리는 현상이 있었습니다. 본 논문도 Transformer보다 뒤에 나온 논문이지만, Transformer가 아닌 Seq2seq 기반으로 모델을 구성한 것을 볼 수 있습니다. 단, Transformer를 제안한 「Attention Is All You Need」 논문에서 제안된 **Multi-Head Attention**을 사용했습니다. 또한 뒤에서 다룰 **Word-Piece Model (WPM)**, **Scheduled Sampling (SS)**, **label smoothing**, **Asynchronous SGD**, **language model** 등을 사용했습니다. 자세한 내용은 뒤에서 다루겠습니다.

## System Overview

### Basic LAS Model

![las-model](https://postfiles.pstatic.net/MjAyMDAzMjRfMzgg/MDAxNTg1MDI5MjUyNzIx.A_WNIScwOfaYzJad-l7Hd62NVOkizEQZQhla-zH-lGUg.wwiDAnHkhNJmd_pVcs8sCp4mC68pxGpIDPb7dOvDJW4g.PNG.sooftware/image.png?type=w773)  

LAS 모델을 간략하게 설명해줍니다. Encoder(Listener)는 입력으로 들어온 특징 벡터를 ***h***라는 higher-level feature로 변환해줍니다. 이러한 ***h***를 가지고 Decoder(Speller)는 어텐션 매커니즘과 함께 출력을 만들어 냅니다. 이에 대한 자세한 설명은 [「Listen, Attend and Spell」 Paper Review](https://github.com/sh951011/Paper-Review/blob/master/Review/Listen%2C%20Attend%20and%20Spell.md)을 참고하시면 좋을 것 같습니다.

### Word-Piece Models

LAS 모델은 아웃풋의 단위가 보통 grapheme (character)이였습니다.  
  
하지만 이러한 구조는 OOV (Out-Of-Vocabulary) 문제가 발생시킬 수 있습니다. 이를 위한 대안으로, grapheme 단위가 아닌 phoneme (음소) 단위가 있습니다만, phoneme 단위의 단점은 추가적인 발음 모델과 언어 모델이 필요하다는 점입니다. 또한 본 논문에서 실험한 바로는, phoneme 단위는 grapheme 단위 모델보다 성능이 좋지 못했다고 합니다.
  
그래서 본 논문은 Word-Piece Model (WPM)을 사용했다고 합니다. WPM은 OOV 문제를 해결할 수 있습니다. 또한, 일반적으로 word-level의 언어 모델은 graphme-level의 언어 모델보다 Perplexity가 낮다고 합니다. (Perplexity가 낮을수록 우수한 모델입니다.) 그래서 본 논문에서는 이러한 경향을 봤을 때, WPM을 사용하게 되면 디코딩 과정에서 더 우수한 성능이 나오지 않을까라고 예상했다고 합니다. 
  
또한 이러한 WPM으로 진행하게 되면, 기존 문자 단위에 비해 더 적은 디코딩 스텝으로 계산되기 때문에 학습 및 추론 속도가 향상되는 장점도 가지게 됩니다. 그리고 결과적으로, WPM을 사용한 모델이 다른 모델보다 더 좋은 성능을 보였다고 합니다.
  
주의할 점으로 Word-Piece 같은 경우, 한국어에서는 오히려 성능이 저하된다고 합니다. 
  
### Multi-Head Attention
  
![MHA](https://postfiles.pstatic.net/MjAyMDAzMjRfMTQ2/MDAxNTg1MDI5MjY0MTU1.UHNwxE6qRO7tM9SrtoPhXoZz-thBq8hLzIgCkokhbe0g.kRmkmI0X3ZCu-AVN9CPpAH4JjPW1GSSFmvl9xRRsQKkg.PNG.sooftware/image.png?type=w773)

Multi-Head Attention (MHA)은 유명한 「Attention Is All You Need」 논문에서 기계번역 분야를 위해 제안되었습니다. 본 논문은 이러한 MHA를 Speech 분야로 확장해보았다고 합니다.   
  
![attn-distribution](https://postfiles.pstatic.net/MjAyMDAxMjVfMTIg/MDAxNTc5ODg4NDkxMDQz.miNLNdmdj0t3Ll12purypbOIE6PWRFijlxAF4ci5K28g.c-UT98v0QJumGmehmlwGkQ0bQxxV_jCKOCjOVH17ZcYg.PNG.sooftware/image.png?type=w773)

MHA는 기존의 어텐션을 multiple head로 확장한 구조입니다. 기존 어텐션이 1개의 어텐션 분포를 만들었다면, MHA의 각 head는 서로 다른 어텐션 분포를 만들어 내게 됩니다. 이러한 구조는 각 head가 encoder output의 서로 다른 곳을 Attend하게 해주는 효과가 있습니다. 
  
본 논문에서는 MHA를 적용 전, 후를 따로 비교하지는 않을 것 같습니다만, 제가 진행하는 음성 인식 프로젝트에서 비교해본 결과 MHA를 적용했던 모델이 압도적으로 좋은 성능을 보였습니다.
  
