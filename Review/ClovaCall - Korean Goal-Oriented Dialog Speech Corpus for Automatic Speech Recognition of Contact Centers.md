# ClovaCall: Korean Goal-Oriented Dialog Speech Corpus for Automatic Speech Recognition of Contact Centers  
  
![image](https://user-images.githubusercontent.com/42150335/80241423-8a367180-869e-11ea-8438-6b651ab65fb6.png)  
  
[논문링크](https://arxiv.org/abs/2004.09367)

2020-04-20에 클로바에서 공개한 따끈따끈한 논문입니다. 한국어 음성 데이터셋 공개와 더불어 베이스라인 코드와 AI Hub, 공개한 데이터셋에 대한 학습 결과까지 포함하고 있습니다. 현재 제가 진행하는 프로젝트와 완전히 동일한 주제이면서도 같은 데이터셋 (AI Hub) 을 이용한 학습까지 했다고하니 굉장히 기대하면서 읽었습니다. 게다가 논문을 낸 기관이 네이버 Clova여서 더 기대가 됐네요.  

## Abstract  

ASR은 여러 어플리케이션에서 필수적입니다만, License-free한 데이터는 찾기 힘들고, 유명한 Switchboard와 같은 데이터는 조금 구식입니다. 또한 가장 큰 문제점은 이러한 오픈 데이터는 대부분 영어로 이루어져 있다는 점입니다. 그래서 본 논문에서는 대용량의 한국어 음성 데이터셋을 공개한다고 밝힙니다. 11,000명의 화자에게서 얻은 60,000 쌍의 음성 데이터셋입니다. (1,000시간의 AI Hub 데이터셋이 2,000명의 화자로 이루어진 점과 비교하여 다양한 화자들로 구성된 데이터셋임을 알 수 있습니다.) 또한 해당 데이터셋을 검증하기 위한 베이스라인 코드를 같이 공개했습니다. 해당 데이터셋 및 코드는 [이곳](https://github.com/ClovaAI/ClovaCall)에 공개되어 있습니다.  

## 1. Introduction
  
음성인식 서비스는 다양한 분야에 적용가능한 핵심 기술입니다. 하지만 이러한 음성인식 서비스 개발을 위한 오픈 데이터들은 (Wall Street Journal (WSJ), TIMIT, Switchboard, CallHome, Librispeech) 공개된 지 오래된 구식의 데이터들이며, 모두 영어로 이루어져 있습니다. 물론 [AI Hub](http://www.aihub.or.kr/aidata/105)와 [zeroth](https://github.com/goodatlas/zeroth)와 같이 오픈된 한국어 음성 데이터셋도 있지만, 이 데이터셋은 일상대화와 같은 주제들을 다룬 데이터셋입니다. 이러한 데이터셋들을 사용하게 되면 특정 도메인을 타겟으로 한 태스크에서는 성능이 좋지 않습니다. 그래서 본 논문에서는 음식점을 도메인으로한 데이터셋을 공개했다고 밝힙니다. 대부분의 문장은 10초 이내의 짧은 발화로 구성되어 있으며, End-point detection이나 alignment가 이슈가 되지 않는다고 합니다.  

또한 본 논문에서는 이러한 데이터셋이 어느 정도의 성능을 낼 수 있는지를 보이기 위해 Deep Speech 2 (DS2)와 Listen, Attend and Spell (LAS)의 2개의 모델로 실험을 진행했다고 밝힙니다. 이때 **Pretraining-finetuning**, **from-scratch training**, **scratch training with data augmentation** 의 3가지 방법을 통해 비교했다고 합니다. 이에 더하여, 비교를 위해 이미 공개되어 있는 2개의 한국어 음성 데이터셋에 대해서도 같이 실험을 진행했습니다. 2개의 데이터셋은 QA Dataset (task-specific)과 AI Hub Dataset (dialog)를 의미합니다.   
  
## 2. Related Work
  

  
