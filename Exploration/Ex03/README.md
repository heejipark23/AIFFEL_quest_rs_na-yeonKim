# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 김나
- 리뷰어 : 박희지


# PRT(Peer Review Template)
- [X]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    1) ResNet-34, ResNet-50의 블록함수 구현이 제대로 진행되었으며 summary가 예상된 형태로 출력되었다.
    <img width="600" height="596" alt="image" src="https://github.com/user-attachments/assets/d572fe39-ccb1-4022-9355-4b412b85cc1d" />
    <img width="600" height="596" alt="image" src="https://github.com/user-attachments/assets/174a5b80-2011-4b65-b340-695462b28c45" />

    2) torchvision의 `OxfordIIITPet` 데이터셋으로 ResNet34/50, Plain34/50 총 4개 모델 모두 epoch이 진행됨에 따라 loss가 감소함을 로그와 그래프로 확인하였다.
    <img width="600" height="412" alt="image" src="https://github.com/user-attachments/assets/357324db-153a-4868-b661-d714cc13739c" />

    3) 동일 epoch=15 기준, Data Augmentation 유/무별 4개 모델의 Train Acc / Best Val Acc / 학습시간을 표로 정리하여 비교하였다.
    <img width="600" height="207" alt="image" src="https://github.com/user-attachments/assets/4ed7678e-5c58-4256-9883-11d56954c273" />

    
    
- [X]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 가장 핵심적인 블록은 `ResNet` 공통 클래스다. `Bottleneck`, `BasicBlock`, `PlainBottleneck`, `PlainBasicBlock` 네 종류의 블록을 `block_type`으로만 갈아끼워 ResNet34, ResNet50, Plain34, Plain50 네 개 모델을 하나의 클래스로 처리하고 있어서, 난이도가 가장 높고 이해가 까다로운 지점이라고 판단했다. 특히 downsample을 언제, 어느 블록에 붙일지 결정하는 조건문이 핵심이다.
    클래스 상단에 Stem에서 layer1~4를 거쳐 avgpool, fc로 이어지는 전체 흐름을 ASCII 다이어그램 주석으로 그려두어서, 코드를 읽기 전에 전체 구조를 먼저 파악할 수 있었고, `_make_layer` 내부에도 채널 수나 크기가 바뀌는 경우 downsample이 필요하다는 이유를 짧게 짚어주는 주석이 달려 있어 코드를 이해하기 쉬웠다.
    <img width="600" height="602" alt="image" src="https://github.com/user-attachments/assets/08fe1041-cb79-49f8-9a45-4616d9a8f111" />

        
- [x]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - "6. 문제점 파악하기" 섹션에서 최초 학습 결과를 보고 ResNet34는 과적합, ResNet50은 데이터셋에 비해 모델이 과도하게 복잡해 학습이 제대로 안 됨, Plain34와 Plain50은 동일 깊이의 ResNet 대비 성능이 크게 떨어진다는 점을 모델별로 원인을 나누어 기록했다. 이어서 "7. 데이터셋 수정하기" 섹션에서 이 문제를 해결하기 위해 Augmentation을 적용했고, 증강된 데이터로 다시 학습시켜 개선 여부를 검증했다. 
    <img width="600" height="476" alt="image" src="https://github.com/user-attachments/assets/4bdb0532-1122-47c8-8a7e-71f408f68760" />

        
- [x]  **4. 회고를 잘 작성했나요?**
    - 마지막에 프로젝트를 진행하며 배운 세 가지가 기록되어 있다. 이번 실험의 한계와 아쉬운 점을 함께 작성하였다.
    - `ResNet` 클래스 상단에 Stem에서 layer1~4를 거쳐 avgpool, fc로 이어지는 구조를 ASCII 다이어그램으로 표현하여 전체 코드 실행 플로우를 나타내었다. 이 다이어그램을 통해 모델 구조를 이해하기 좋았다.
    <img width="600" height="132" alt="image" src="https://github.com/user-attachments/assets/77be4719-6a51-48be-82cc-36135e2c73dc" />

        
- [x]  **5. 코드가 간결하고 효율적인가요?**
    - 블록 클래스와 이를 인자로 받아 공통 처리하는 `ResNet` 클래스, 그리고 `build_resnet34`/`build_resnet50`/`build_plain34`/`build_plain50` 생성 함수로 이어지는 구조는 모델 정의 부분에서 중복을 최소화하고 모듈화가 잘 되어 있었다.
    - 그러나 모델과 데이터로더를 인자로 받는 학습 함수 하나로 묶었다면 코드 길이와 중복을 훨씬 줄일 수 있었을 것 같다.


# 회고(참고 링크 및 코드 개선)
```
모델 구조처럼 복잡한 클래스를 다이어그램으로 표현해 주신 부분이 인상 깊었습니다. 저또한 과적합 문제가 나타났는데, 다양한 augmentation 기법을 적용해 해결하신 과정을 보면서 저도 추가로 적용해봐야겠다는 생각이 들었습니다.
```
