# How MDL Works

**일반화는 압축이다 — 가중치에 담긴 정보가 훈련 출력에 담긴 정보보다 훨씬 적어야 한다.** Hinton & van Camp(1993)의 「Keeping Neural Networks Simple by Minimizing the Description Length of the Weights」(COLT 1993) 식 (1)~(27)을 브라우저에서 하나씩 계산해 보는 인터랙티브 교육 자료입니다. 가중치와 오차를 비트로 보내는 통신 문제에서 출발해, 가중치를 가우시안 노이즈가 낀 분포로 바꾸고 그 비용을 KL 발산으로 셈하는 방법, 그리고 그것이 오늘날 변분 추론(Bayes by Backprop, ELBO)의 출발점이 된 과정을 따라갑니다.

🔗 **[데모 바로가기](https://dev-jonghoonpark.github.io/how-mdl-works/)**

## 다루는 내용

1. **일반화 = 압축** · 송신자와 수신자, 다항식 차수별 가중치 비트 + 미스핏 비트. MDL이 고른 차수가 참 함수 오차가 가장 작은 차수와 겹침
2. **오차를 비트로 바꾸기 (식 1~3)** · 그림 1 재현(확률 질량 = 높이 × 폭), 약속한 σ가 미스핏의 RMS일 때 비트가 최소
3. **가중치 감쇠와 정밀도의 낭비 (식 4)** · 가중치 감쇠 = 조잡한 MDL, 가중치별 최적 양자화 폭 t² = 12σ̂²/s로 15비트 가까이 절약
4. **노이즈 낀 가중치** · 3차 다항식에서 KL과 미스핏의 저울질, 가중치별 최적 σ가 베이즈 사후 정밀도와 같아지는 것
5. **bits-back 논증 (식 5~9)** · 가중치를 실제로 뽑아 보내고 환불받기, 양자화 폭과 무관하게 평균 순비용이 KL로 수렴
6. **노이즈를 은닉층에 통과시키기 (식 10~14)** · 논문의 2차원 표를 그림으로, 몬테카를로·1차 테일러 근사와 비교
7. **데이터가 정하는 사전분포 (식 15~25)** · 혼합 사전분포의 정확한 KL과 자유 에너지 상한 Ĝ, 선택 비용·표본 비용·bits back 분해
8. **브라우저에서 학습** · 벌점 없음 / 가중치 감쇠 / MDL 노이즈 가중치(논문 9절 초기화, 5성분 적응형 혼합, β 점진 증가)를 동시에 학습. β를 1로 고정하면 논문처럼 정보 없는 해로 붕괴(데이터 8가지 모두 상대 오차 ≈ 1.0), 점진 증가면 8가지 중 7가지가 0.045~0.059. 데이터 8가지의 결과표 포함
9. **논문의 실험 결과** · 펩타이드 과제(입력 128, 훈련 105, 가중치 521) 상대 오차 0.286 vs 가중치 감쇠 0.317 vs 벌점 없음 0.967, 그리고 설명 길이가 가장 짧았던 해가 상대 오차 ≈ 1.0이었던 “당혹스러운” 결과
10. **그다음** · 음의 ELBO와의 등식, Graves(2011), Bayes by Backprop, 국소 재매개변수화, KL 어닐링, PAC-Bayes. 정확한 기대 오차 vs 몬테카를로 추정 비교
11. **퀴즈** 7문항

## 참고

- Hinton & van Camp (1993), *Keeping Neural Networks Simple by Minimizing the Description Length of the Weights*, COLT 1993 — [PDF](https://www.cs.toronto.edu/~hinton/absps/colt93.pdf)
- Graves (2011), *Practical Variational Inference for Neural Networks*, NIPS 2011
- Blundell 외 (2015), *Weight Uncertainty in Neural Networks*, ICML 2015 — [arXiv:1505.05424](https://arxiv.org/abs/1505.05424)

[how-ai-works](https://github.com/dev-jonghoonpark/how-ai-works) 시리즈의 일부입니다.
