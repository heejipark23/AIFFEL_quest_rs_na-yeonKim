# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 김나연
- 리뷰어 : 조영근

# PRT(Peer Review Template)
- [X]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 시각화 요구사항이 정확하게 이루어졌는가?
      
      프로젝트1, 2에서 요구하고 있는 데이터개수 시각화가 잘 되었음

      또한 예측결과 시각화도 잘 진행 되었음
      
```
# 예측값과 정답을 시각화해서 비교해보기

import matplotlib.pyplot as plt

plt.scatter(X_test[:, 0], y_test)
plt.scatter(X_test[:, 0], prediction)
plt.show()
```      
<img width="549" height="410" alt="image" src="https://github.com/user-attachments/assets/afdfb228-96ee-4900-9c80-60ea63764b0a" />

```
# year, month, day, hour, minute, second 데이터 개수 시각화하기
# [
#  [ax1, ax2, ax3],
#  [ax4, ax5, ax6]
# ]

import matplotlib.pyplot as plt
import seaborn as sns

fig, axs = plt.subplots(2, 3, figsize=(18, 10))
cols = ['year', 'month', 'day', 'hour', 'minute', 'second']
for ax, col in zip(axs.flatten(), cols):    # (ax1, year), (ax2, month), ..., (ax6, second)
    sns.countplot(x=col, data=train, ax=ax) # 컬럼의 빈도수 그래프를 그림
    ax.set_title(f'Countplot of {col}')
plt.tight_layout()   # 겹치지 않게 간격 조정
plt.show()
```
<img width="849" height="473" alt="image" src="https://github.com/user-attachments/assets/66b48b27-2cac-42f6-843b-c2550a24d6dc" />

```
fig, axs = plt.subplots(1, 2, figsize=(16, 6))

# temp vs count 시각화
axs[0].scatter(X_test['temp'], y_test, color='blue', label='Actual')
axs[0].scatter(X_test['temp'], y_pred, color='red', label='Predicted', alpha=0.5)
axs[0].set_xlabel('temp')
axs[0].set_ylabel('count')
axs[0].set_title('Temperature vs Count')
axs[0].legend()

# humidity vs count 시각화
axs[1].scatter(X_test['humidity'], y_test, color='blue', label='Actual')
axs[1].scatter(X_test['humidity'], y_pred, color='red', label='Predicted', alpha=0.5)
axs[1].set_xlabel('humidity')
axs[1].set_ylabel('count')
axs[1].set_title('Humidity vs Count')
axs[1].legend()
```
<img width="850" height="372" alt="image" src="https://github.com/user-attachments/assets/beaff62e-cad3-4347-accf-dca4bb8e816e" />



   - 프로젝트 2의 회귀모델 예측정확도가 기준 이상 높게 나왔는가?
     
      RMSE 값 150 이하를 달성을 요구하였고 RMSE: 141.2865946027274을 달성 하였음
```
# 학습시킨 모델로 예측하고 손실함수 계산하기

from sklearn.metrics import mean_squared_error
import numpy as np

y_pred = model.predict(X_test)
mse = mean_squared_error(y_test, y_pred)
rmse = np.sqrt(mse)
print("MSE:", mse)
print("RMSE:", rmse)
```  
<img width="187" height="47" alt="image" src="https://github.com/user-attachments/assets/39688cc1-9723-4f30-90e5-8cb660e3f3ea" />


   - 프로젝트 1의 회귀모델 예측정확도가 기준 이상 높게 나왔는가?
     
      MSE 손실함수값 3000 이하를 달성하지 못 하였음
     
     학습률을 변경하여 MSE 함수의 손실값을 3000이하로 맞추어야 하는데 오차률이 너무 큼
     
```
     # 학습률 설정 (하이퍼파라미터)
     LEARNING_RATE = 0.001
```
   <img width="268" height="140" alt="image" src="https://github.com/user-attachments/assets/05eacce9-ae5d-42ac-869a-ce14925d6ac6" />


- [X]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 해당 코드 블럭을 왜 핵심적이라고 생각하는지 확인
    - 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
    - 해당 코드의 기능, 존재 이유, 작동 원리 등을 기술했는지 확인
    - 주석을 보고 코드 이해가 잘 되었는지 확인 <br><br>
     
      
    <img width="496" height="176" alt="image" src="https://github.com/user-attachments/assets/c04b2155-a35f-411c-a917-33179776d3fd" />

        
- [ ]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - 문제 원인 및 해결 과정을 잘 기록하였는지 확인
    - 프로젝트 평가 기준에 더해 추가적으로 수행한 나만의 시도, 
    실험이 기록되어 있는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        
- [ ]  **4. 회고를 잘 작성했나요?**
    - 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
    배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
    - 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
        - 중요! 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부
        
- [X]  **5. 코드가 간결하고 효율적인가요?**
    - 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
    - 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화/모듈화했는지 확인 <br><br>


  <img width="496" height="313" alt="image" src="https://github.com/user-attachments/assets/44b10a18-80d2-4433-92ff-464717bb0729" />


# 회고(참고 링크 및 코드 개선)
```
# 리뷰어의 회고를 작성합니다.
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
