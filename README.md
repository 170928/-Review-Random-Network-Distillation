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


[Method]
**Exploration Bonus**  
기존의 환경에서 주는 reward rt를 아래 그림과 같이 intrinsic reawrd it 를 더하는 것으로 대체합니다.  
![2](./img/2.PNG)  
이때, Exploration Bonus는 Agent가 기존에 방문한적 없는 State에 도달 할 수 있도록 만드는 것이 목적이므로 기존에 방문했던 State에 도달하였을 때 보다 새로운 State에 도달하면 높은 값을 주도록 해야 합니다.  
환경을 크게 2가지로 나누어서 논문에서는 이전 연구들에 대해서 설명합니다.  
1. Tabular Setting : State의 수가 finite 하기 때문에 state 별로 방문했던 횟수를 count하고 방문 횟수가 늘어날 수록 intrinsic reward가 줄어드는 함수를 설정  
2. Non-Tabular Setting : State 를 대부분 한 번만 방문하기 때문에 방문했던 횟수에 대한 count는 적절하지 못합니다. 그러므로, state density esimation의 변화를 instrinsic reward로 사용하는 방법 (Reference : Marc Bellemare, Sriram Srinivasan, Georg Ostrovski, Tom Schaul, David Saxton, and Remi Munos. Unifying count-based exploration and intrinsic motivation. In NIPS, 2016.)  

**Random Network Distillation**  
이 논문에서 제시하는 방법인 RND는 다음과 같이 2가지 neural network를 활용합니다.  
1. a ﬁxed and randomly initialized target network.   
![3](./img/3.PNG)
2. a predictor network trained on data collected by the agent.   
![4](./img/4.PNG)

이때, predictor network는 MSE 를 최소화하는 방향으로 학습을 하여 새로운 state를 만나게 되었을 때 prediction error가 큰 network가 되도록 합니다.
![5](./img/5.PNG)

**Source of Prediction Errors**
이 논문에서는 이런 Prediction error가 발생하는 요소에 대해서 다음과 같이 정리합니다.  
1. Amount of training data : predictor에 의해서 몇번 경험하지 못한 경우
2. Stochasticity : target function 이 stochastic 이기 때문에 예측의 불확실성이 높은 경우
3. Model misspeciﬁcation : 예측에 필요한 necessary information 이 부족하거나 the model class가 the complexity of the target function을 충족시키기에 부족한 경우.
4. Learning dynamics : predictor가 학습과정에서 target function을 근사하는 것에 실패한 경우

이 중 1번째 요소는 exploration bonus로 활용할 수 있습니다. 실제로 prediction error가 발생하는 이유는 위의 요소들의 종합적인 이유이지만 모든 요소가 bonus로 여기기에 좋지는 않습니다. 
2번 요소의 경우 'noisy-TV' 문제로 유명한 문제이며 2번과 3번 요소를 해결하기 위해서 새로운 데이터 포인트를 볼 때 예측 모델이 얼마나 향상되는지 측정하는 연구 방법들이 있었으나 계산 측면에서 효율적이지 못하였습니다. (Reference : Schmidhuber (1991a); Oudeyer et al. (2007); Lopes et al. (2012); Achiam & Sastry (2017) )  



