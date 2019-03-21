# -Review-Random-Network-Distillation
> https://arxiv.org/abs/1810.12894
> https://bluediary8.tistory.com/37


[Review &amp; Implementation]
![1](./img/1.PNG)

[Summary]
RND 논문은 Deep reinforcement learning을 통해 Agent를 학습할 때 적은 computation overhead로 exploration bonus를 줄 수 있는 방법을 소개하는 논문입니다. Explration bonus 라는 개념을 Intrinsic reward로 표현하며 이를 fixed randomly initialized neural network가 예측한 state feature와 실제 state feature의 오차로 정의 하였습니다. RND 기법이 가지는 장점을 다음과 같이 얘기하였습니다.  
1. 기존에 존재하는 RL 기법들에 모두 적용이 가능  
2. single forward 계산을 통해서 Intrinsic reward를 계산
3. high-dimensional observation에 효과적



