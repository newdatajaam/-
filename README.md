## 멀티모달을 활용한 유사도 기반 국내 관광 정보 검색 시스템
(마지막 수정 : 24.07.09)

## Tacademy ASAC 4기 기업연계프로젝트
* 프로젝트 명: 멀티모달을 활용한 유사도 기반 국내 관광 정보 검색 시스템(A similarity-based domestic tourism information search system using multimodal)
* 기간 : 2024.03.05 ~ 2024.05.20
* 팀원 : 신재함, 이현수, 장서연, 한은경       
<br></br>

## 프로젝트 개요(Project Overview)
1. 기존 서비스의 한계
   * 기존 관광지 검색 서비스는 대부분이 텍스트를 기반으로 검색 결과를 제공
   * 일부 이미지 검색 서비스 또한 이미지에 부여된 제목 등의 메타정보 등을 통한 검색이 대다수
   * 그 외 기존 서비스들은 Text to Image 혹은 Image to Text 등 학습된 단방향으로만 검색 제공
2. 프로젝트 목표
   * 양방향 검색을 통해 Text, Image를 자유롭게 입력값으로 활용가능하고,
   * 검색 결과 또한 Text, Image의 맥락을 고려한 검색 결과 가능한 시스템 개발
   * 학습을 통해 학습되지 않은 해외 관광지와 유사도가 높은 국내 관광지 추론이 가능한 모델 완성
<br></br>

## 데이터 (Data)
* [DACON 2022 관광데이터 AI 경진대회 train.csv](https://dacon.io/competitions/official/235978/data")
  
![image](https://github.com/newdatajaam/Domestic-Tourism-Search-System-with-Multimodal/assets/152856364/93684f16-2251-493b-a989-fc5e3ecd98d6)
<br></br>

## 프로젝트 진행단계
멀티모달 기술을 활용한 프로젝트 진행
* 각 모달별로 임베딩 과정을 거쳐 비정형 데이터를 벡터 값으로 변환
* 두 데이터가 동일한 정보를 가진 데이터임을 알 수 있도록 새로운 동일한 공간에 두 벡터 값을 투영
    1. 텍스트 임베딩
    2. 이미지 임베딩
    3. 조인트 임베딩
<br></br>

## 모델 평가
1. 텍스트 임베딩
   * 기존 Average Precision @K 평가 지표를 응용하여 유사도 기반 검색 결과의 검색 순위에 따라 가중치를 부여하여 정량적 평가 진행
   * 코사인 유사도를 참고하여 질의에 대한 답변을 정성적으로 판단하여 평가(Weighted Average Precision @K : AP@K)
2. 이미지 임베딩
   * 이미지에 대한 라벨링을 기존 데이터 셋에 있는 카테고리 라벨링에 따라 분류 모델링 진행
   * 질의(query) 이미지에 대한 분류 예측에 대한 accuracy 평가 적용
   * 정성적인 이미지 유사도 평가
3. 조인트 임베딩
   * TEXT, Image 데이터가 한 공간에 투영되었는지 확인하기 위해 두 벡터 값의 코사인 유사도, 유클리디안 유사도(유클리디안 거리) 활용하여 모델 평가 진행
   * 질의(Query)와 검색 결과간의 코사인 유사도를 통해 정성적 평가 적용
   * 질의(Query)에 대한 검색 결과 Label 일치도에 대한 Accuracy, 전체데이터에 대한 Weighted Precision 평가 진행
<br></br>

## 결과
### 결과1. 기술통계량 비교 결과 
절대적 변화량 기준 
  * 코사인 유사도: 0.7814 증가
  * 유클리디안 유사도: 0.75424 증가
![image](https://github.com/newdatajaam/Domestic-Tourism-Search-System-with-Multimodal/assets/152856364/2320691f-aba0-47bd-ab6a-047d5be78c4f)

### 결과2. TSNE 벡터 시각화 결과
기존 각 모달리티(텍스트, 이미지)의 벡터 분포도를 겹쳐서 확인한 결과
![image](https://github.com/newdatajaam/Domestic-Tourism-Search-System-with-Multimodal/assets/152856364/9e330bf2-f6da-4975-b843-bef19905e899)

### 결과3. 내부데이터 자체 query 평가(acc, weighted precision)
모델별(텍스트, 이미지, 멀티모달(조인트)) 내부 데이터 검색 향상도 비교 결과
- 평가기준
    * Acc: Query Label과 상위 10개 검색 결과의 Label의 정확도
    * Weighted Precision: Query Label과 상위 10개 검색 결과의 Label의 정밀도
      (이때 가중치는 상위 결과일수록 높고 단계별로 내려감 / 결과1위 = 10/55, ..., 결과10위 = 1/55 등)
- 결과

   ![image](https://github.com/newdatajaam/Domestic-Tourism-Search-System-with-Multimodal/assets/152856364/62e8cc48-00e4-45e9-876f-f84322c0cd79)


결과3 참고자료

![image](https://github.com/newdatajaam/Domestic-Tourism-Search-System-with-Multimodal/assets/152856364/6d0dcf8a-d232-48e7-b024-6b51972a90bd)

<br></br>

