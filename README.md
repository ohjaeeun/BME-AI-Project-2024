# Parkinson Disease Prediction Multimodal Model
[24-1 HUFS BME 의료영상처리 이론 및 실습] \
**team member** : 곽준무, 양아연, 오재은, 이근혜

- 이 프로젝트는 `Multi Modal Deep Learning을 활용한 Parkinson's disease Prediction Model`을 생성하는 프로젝트입니다.
- MDVP(Multi Dimension Voice Program)에서 자주 사용하는 주파수 성분만을 파킨슨 질환의 환자와 정상인의 음성으로부터 추출한 텍스트 데이터와 파킨슨 질환의 환자와 정상인의 손그림 이미지를 증강시킨 데이터를 사용하였습니다.
## 목표
- 두 종류의 데이터를 input으로 하여 실생활에서 파킨슨 질환일 확률을 예측하여 조기 진단을 보조할 수 있는 인공지능 모델을 개발하고자 하였습니다.
- 여러 요소들로부터 해당 질환일 확률을 판별하고자 하는 목적으로 특정 상황이 아닌 다양한 상황에서도 모델의 일반화 능력을 가질 수 있도록 하였습니다. 

## Dataset
- Audio data https://www.kaggle.com/datasets/debasisdotcom/parkinson-disease-detection/data 
   * total 197 data
   * MDVP:Fo(Hz), MDVP:Fhi(Hz), MDVP:Flo(Hz), MDVP:Jitter, MDVP:Shimmer 등의 column
   * label - healty: 0 (50), parkinson's positive: 1 (147)

- Image data https://www.kaggle.com/datasets/banilkumar20phd7071/handwritten-parkinsons-disease-augmented-data
  * original data: total 204 images
  * aumented data: total 3264 images
  * 2-classes of healthy and parkinson's positive
  
## Algorithm
- Multi Modal Deep Larning (Late Fusion)
>  ![image](https://github.com/user-attachments/assets/21e20797-83cc-461b-ad03-b9c93d02ba7b)
  - Input data
    - audio data (csv), drawing data (image)
  - Output
    - Predicted parkinson probability
  
## Model
- Model 1 + Model 2 -> Late Fusion 
![image](https://github.com/user-attachments/assets/67581fb1-6b6a-401a-84e1-577694a728ac)
- Parameters
  - Learning rate = 0.0001
  - batch size = 32
  - Epoch number = 70
  - Loss function = categorical crossentropy
  - Optimizer = Adam
   
- 음성 입력: Dense 레이어를 통해 음성 주파수 데이터를 처리
- 이미지 입력: EfficientNetB0을 사용하여 이미지 데이터를 처리
- 결합: 두 입력의 출력을 결합 → 0.5 이하: 정상 / 0.5 이상: 파킨슨병 환자

## Result
Validation Loss: 0.59 / Validation Accuracy: 0.77

## Evaluation
![image](https://github.com/user-attachments/assets/08edaef2-7f16-4c02-849c-2df925de908d)



## Test
- 팀원 1명의 손그림 + 녹음된 voice의 feature 추출
 >  ![image](https://github.com/user-attachments/assets/2e885574-844f-4f39-b808-b4153c9efe39)
 >  ![image](https://github.com/user-attachments/assets/d725c438-32ad-46b0-884a-bf1b62fd20b4)
- 예측 결과
> ![image](https://github.com/user-attachments/assets/89651e48-2138-4670-b6f2-046eb149d935)


## 실행방법

#### Colab에서 실행하는 법
1. 아래의 link를 눌러 사용하고자 하는 모델의 Code를 Colab에서 확인할 수 있다.
- Audio Classification Model
https://colab.research.google.com/drive/1lNuHnLJXoyemU8RfoJaCnO_w5oCImk4r?usp=sharing

- Image Classification Model
https://colab.research.google.com/drive/1EnUqNLi9zFixI8RZAbJqsnrVQ2ncqHaE?usp=sharing

- Multi Modal DL Model
https://colab.research.google.com/drive/12bVquFnzTCrBCKI9R6CvhM_kTAb-zFl4?usp=sharing

2. Dataset을 다운 받아 Colab에서 실행한다.
-  audio data
https://www.kaggle.com/datasets/debasisdotcom/parkinson-disease-detection/data

- Image data
https://www.kaggle.com/datasets/banilkumar20phd7071/handwritten-parkinsons-disease-augmented-data
