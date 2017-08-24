# Stochastic Gradient Descent

## 소개 
#### 특징
- 심플하다.
- 선형 분류기 학습에 매우 효율적인 접근이다 
주석* SVM(Support Vector Machines)과 Logistic Regression같은 convex loss function하에서 특징적인 선형 분류기에 대해 배우기 매우 효율적인 접근이다.

#### SGD is
- 텍스트 분류와 자연어 분류에서 가끔 마주치는 large-scale 그리고 분포정도가 드문 머신러닝 문제에 성공적으로 적용되어 왔다.

#### 장점
- 효율적이다.
- 쉬운 구현

#### 단점
- regularization parameter 그리고 반복되는 숫자와 같은 많은 hyperparameters가 요구된다.
- feature scaling에 민감하다.

주석* 튜닝 또는 최적화 해야 하는 주 변수가 아닌 사람들이 선험적 지식으로 설정을 하거나 또는 외부 모델 메커니즘을 통해 자동으로 설정이 되는 변수를 말한다.


## Classification

SGDClassifier 클래스는 특이한 손실함수와 분류에 패널티를 지원하는 평범한 통계학적 경사하강법을 배우는 일반적인 방법을 구현합니다.

#### 다른 분류기처럼 SGD는 2개의 배열에 맞춰져 있습니다.
  - X배열 : [n_samples, n_features] 사이즈의 훈련 샘플
  - Y배열 : [n_samples] 사이즈의 타겟 밸류(target values, class labels)를 가지는 훈련 샘플

```
>>> from sklearn.linear_model import SGDClassifier
>>> X = [[0., 0.], [1., 1.]]
>>> y = [0, 1]
>>> clf = SGDClassifier(loss="hinge", penalty="l2")
>>> clf.fit(X, y)
SGDClassifier(alpha=0.0001, average=False, class_weight=None, epsilon=0.1,
       eta0=0.0, fit_intercept=True, l1_ratio=0.15,
       learning_rate='optimal', loss='hinge', n_iter=5, n_jobs=1,
       penalty='l2', power_t=0.5, random_state=None, shuffle=True,
       verbose=0, warm_start=False)
```

#### 내부 멤버 메소드
  - predict : 피팅된 후에 모델은 새로운 값을 예측하여 보여준다.
  - coef_ : 모델의 파라미터를 보여준다.
  - intercept_ : offset 또는 bias라고 알려진 intercept를 보여준다.

hyperplane으로의 부호 있는 거리를 얻기 위해서는 SGDClassifier.decision_function을 사용한다.


#### 구체적인 손실함수(loss function)는 loss파리미터를 통해 설정될 수 있다.
SGDClassifier는 다음의 loss functions를 지원한다.
  - loss="hinge" : (soft-margin) 선형 Support Vector Machine
  - loss="modified_huber" : smoothed hinge loss,
  - loss="log" : logistic regression

hinge, modified_huber의 경우는 게으른 손실함수인데(예제가 magin constaint와 충돌이 될 때만 모델 파라미터를 업데이트 한다) 훈련을 매우 효율적으로 만들어주고 L2패널티가 사용되어도 결과적으로 밀도가 매우 희박한 모델을 만들어준다.


#### 백터의 개연성 측정 
loss="log"나 loss="modified_huber"는 샘플 x당 "P(y|x)" 백터의 개연성을 측정할 수 있게 해주는 predict_proba 메소드를 사용할 수 있게 한다.
```
>>> clf = SGDClassifier(loss="log").fit(X, y)
>>> clf.predict_proba([[1., 1.]])                      
array([[ 0.00...,  0.99...]])
```

#### 구체적인 패널티 설정 
구체적인 패널티는 "penalty" 파리미터를 통해 설정될 수 있으며, SGD는 다음의 패널티를 제공한다.
  - penalty="l2": L2 norm penalty on coef_. (기본값으로 설정된다)
  - penalty="l1": L1 norm penalty on coef_.
  - penalty="elasticnet": Convex combination of L2 and L1; (1 - l1_ratio) * L2 + l1_ratio * L1.  

L1패널티는 밀도가 최대 계수를 0으로 이끄는 밀도가 희박한 결과로 이끈다.
The Elastic Net은 큰 상관계수 앞에서 L1 패널티의 약간의 결손계수를 풀어낸다.
"L1_ratio" 파라미터는 L1과 L2패널티의 convex combination을 제어(control)한다.

#### one versus all(OVA)
SGDClassifier는 "one versus all"(OVA) 방식으로 다양한 이진 분류기를 조합함으로써 다중 클래스 분류(multi-class classification)을 지원한다.
K 클래스 각각에 대해, 그와 다른 모든 K-1 클래스를 구별하는 바이너리 분류자가 습득된다.
테스트 시간에 각 분류 기준에 대한 신뢰 점수 (즉, 초평면에 대한 부호가 있는 거리)를 계산하고 가장 높은 신뢰도를 가진 클래스를 선택합니다. 
아래 그림은 iris 데이터 세트에 대한 OVA 접근법을 보여줍니다. 파선(dashed line)은 세 가지 OVA 분류자를 나타냅니다.
배경색은 세 분류 자에 의해 유도 된 결정 표면을 보여줍니다.

멀티 클래스 분류 coef_의 경우는 "shape=[n_classes, n_features]"의 2차원 배열이고 intercept_는 "shape=[n_classes]"의 1차원 배열이다.

coef_의 i 번째 행은 i 번째 클래스에 대한 OVA 분류 자의 가중치 벡터 를 유지한다.
클래스는 오름차순으로 색인됩니다 (속성 참조 ).
원칙적으로 그들은 확률모델을 만들 수 있기 때문에, "loss=log" 그리고 "loss=modified_huber"는 one-vs-all 분류에 보다 적합하다.


#### 피팅 파라미터
SGDClassifier는 "class_weight"그리고 "sample_weight" 피팅 파라미터들(fit parameters)을 통해 편중된 클래스와 편중된 인스턴드 둘다 지원한다.

SGDClassifier평균 SGD (ASGD)를 지원합니다. "average=True" 설정에 의해 평균화를 활성화 할 수 있다.
ASGD는 샘플을 통해서 각각 반복되는 일반 SGD의 계수의 평균화를 통해 동작한다.
ASGD를 사용할 때 학습 속도는 더 크고 일정 할 수도 있습니다. 일부 데이터 세트에서는 훈련 시간이 단축된다.

logistic loss 분류를 위해, 평균화 전략을 하는 다른 변종 SGD는 Stochastic Average Gradient (SAG) 알고리즘을 이용할 수 있으며, 로지스틱 회귀에서 사용할 수 있다.



#### Regression
