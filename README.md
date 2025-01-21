# 퇴사 예측 신경망 모델

<img src="[https://github.com/maango97/hr-analytics/blob/main/%EB%B0%9C%ED%91%9C%20%ED%91%9C%EC%A7%80.png]" width="900" height="480"/>

- 기간 : 2024.10(3인)
- [데이터 출처(Kaggle)](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset)
- [발표 자료 PDF](https://github.com/maango97/hr-analytics/blob/main/%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%20%E1%84%8C%E1%85%A1%E1%84%85%E1%85%AD.pdf)


## 분석 개요


- **문제 정의**
  
  - 높은 퇴사율 -> 신규 채용이나 인력 재배치 등 직접 비용 외에도 업무 공백, 조직 분위기 저하 등 간접적인 피해 발생 -> 기업 손실 증가
  - 퇴사 예측 모델을 만들어 퇴사율 감소를 위한 HR 전략 수립을 돕는 것을 목표로 함
 
- **데이터 전처리**

  - 문자형 컬럼을 수치형으로 인코딩
  - Min-Max 정규화 시행 
  
- **모델링 및 결과**
  
  - 사용 모델 : XGboost, Random Forest, 신경망
  - 정확도 비교 결과 강점을 보이는 신경망 모델을 채택
  - 데이터 불균형 문제: 소수 클래스에 대한 예측 성능이 떨어지는 문제 발생, SMOTE를 이용해 해결
  - 오버 피팅 방지 : 배치 정규화, L2 정규화, 드롭아웃, 얼리스탑핑
  - 모델 성능 개선 : 하이퍼파라미터(은닉층 수, 뉴런 수) 조정, 30개 이상의 파생 변수를 생성 후 하나씩 시도
  - 최종 정확도 : F1-Score = 0.9864 / 훈련 Loss = 0.1374 / 테스트 Loss = 0.1727
    
- **결론**
  
  - **SHAP 분석**을 활용하여 예측에 기여하는 정도가 큰 변수를 찾고 그에 맞는 활용 전략 수립

- **WHY?Moments**
  
  - 신경망 모델을 저장하고 로드 후 실행하면 정확도가 올라가는 현상, 왜?
  
    - Keras의 EarlyStopping 콜백 옵션인 **restore_best_weights** 옵션으로 인해 가장 좋은 성능을 보였던 가중치로 복원되기 때문!

  - 에폭수에 따른 loss를 시각화했더니 특정 구간에서 급격이 loss 값이 증가하는 현상, 왜?
 
    - 신경망이 학습 도중 **local minimum**에 빠졌다가 탈출하는 과정에서 loss 값이 잠시 증가했기 때문!
  

## 환경

- Anaconda - Jupyter Notebook
