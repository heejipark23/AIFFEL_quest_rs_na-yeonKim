# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 김나연
- 리뷰어 : 박희지


# PRT(Peer Review Template)
- [x]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
    - 평가기준 5개 항목이 빠짐없이 체계적으로 구현되어 있음을 확인하였다.
      1) 분석 단계
         <img width="300" alt="image" src="https://github.com/user-attachments/assets/6153296a-eef4-450c-893d-8022491bc3ed" />
      2) 정제 단계
         <img width="300" alt="image" src="https://github.com/user-attachments/assets/9eea384f-3096-409e-a280-7edcea5f3754" />
      3) 데이터셋 분리
         <img width="300" alt="image" src="https://github.com/user-attachments/assets/aab46f9b-0c79-4687-a3dd-795fee8766c0" />
      4) 정규화 및 불용어 제거
         <img width="300" alt="image" src="https://github.com/user-attachments/assets/8024d0be-180d-499a-86e7-ce61ac1526e4" />
      5) 인코딩
         <img width="300" alt="image" src="https://github.com/user-attachments/assets/f7152468-2f5b-48a5-9224-b07e8428f7d1" />

     - train/val loss 감소 경향을 그래프로 확인하여 텍스트 요약 모델이 성공적으로 학습되었음을 확인하였다.
       <img width="500" alt="image" src="https://github.com/user-attachments/assets/b123558c-60f2-45f0-aa45-4445768a67ee" />

     - 두 요약 결과를 문법완성도 측면과 핵심단어 포함 측면으로 나누어 비교·분석하였고, `comparison_df`로 text / headline / attention_summary / summa_summary를 표로 나열하였다.
       <img width="500" alt="image" src="https://github.com/user-attachments/assets/d7694efd-3805-4e12-86c0-0d1c2b5d5965" />
       <img width="500" alt="image" src="https://github.com/user-attachments/assets/2bf15ec3-f602-4db2-a9ca-1d3d94f06f3a" />




    
- [x]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
    - 모델 설계 부분에 Encoder, Decoder, Attention + seq2seq구조를 시각화하여 모델 구조를 쉽게 이해할 수 있었다. 또한, 코드 블록 내부에도 인라인 주석이 붙어 있어 왜 이 코드가 필요한지, 무슨 역할을 하는지를 이해할 수 있었다.
      <img width="500" alt="image" src="https://github.com/user-attachments/assets/0dd7667f-5ff5-46c6-992b-3e79a712da60" />

        
- [ ]  **3. 에러가 난 부분을 디버깅하여 문제를 해결한 기록을 남겼거나
새로운 시도 또는 추가 실험을 수행해봤나요?**
    - 생한 오류와 원인 -> 해결 과정을 작성한 기록과 추가 실험을 없었다.
        
- [ ]  **4. 회고를 잘 작성했나요?**
    - 배운점/아쉬운점/느낀점을 서술한 회고 섹션이 존재하지 않는다.
        
- [x]  **5. 코드가 간결하고 효율적인가요?**
    - 전처리(`preprocess_sentence`), 단어집합 생성(`build_vocab`), 인코딩(`text_to_sequence`), 패딩(`pad_sequences_pytorch`), 학습(`train_model`), 추론(`decode_sequence`, `seq2text`, `seq2headlines`) 등 반복되는 로직을 함수로 잘 분리했다.
    - 모델도 `Encoder` / `Decoder` / `Attention` / `Seq2SeqWithAttention` / `InferenceDecoder` 클래스로 역할이 명확히 나뉘어 있다.


# 회고(참고 링크 및 코드 개선)
```
모델 아키텍처를 시각화해주셔서 이해하기 쉬웠습니다. 또한, vocab_size를 훨씬 작게(src 2,000 / tar 1,000) 구성한 점을 참고할 수 있었습니다. vocab은 손실의 절대값에 큰 영향을 주는 만큼, 이후 loss로 성능을 비교할 때는 vocab 크기 등 전처리 조건을 적절히 설정해야겠다는 점을 배울 수 있었습니다.
```
