---
title: 결정 나무(Decision Tree) 간단 설명
date: 2021-11-04 12:06:48
tags: 
- Python
- Machine Learning
- Decision Tree
- Algorithm
---

## 결정 나무란?

---

**결정 나무** <sup>Decision Tree</sup> 는 분류와 회귀 문제에 널리 사용하는 데이터마이닝 기법이다. 결정 나무는 결정을 하기위해 예/아니오 질문을 연속해가며 학습한다.  

[결정나무 간단설명영상](https://youtu.be/n0p0120Gxqk)  
[결정나무 사이킷런 튜토리얼](https://scikit-learn.org/stable/modules/tree.html#classification)

  
### 결정나무의 의사결정 과정

---

결정 나무가 행하는 이 과정은 '스무고개'를 할때의 그것과 비슷하다.  
사과, 포도, 멜론, 녹차를 구분한다고 생각해보자. 사과와 포도는 과일이고 멜론과 녹차는 과일이 아니다.  
'과일인가요?'라는 질문을 통해 사과, 포도 / 멜론, 녹차를 나눌 수 있고, 사과와 포도는 '(과실 전체의)모양이 둥근가요?', 멜론과 녹차는 '넝쿨에서 자라나요?' 라는 질문을 통해 분류해 낼 수 있다.  
위의 결정나무를 도식화하면 아래와 같다.

![도식화한 결정나무](/images/Decision_Tree/Decision_Tree-1.png)  
  
이렇게 질문에 따라 데이터를 구분짓는 모델을 `결정나무`모델이라고 한다. 한번의 질문에 True 혹은 False를 통해 변수영역을 두 개로 분기한다.  


![모양이 나무를 뒤집어 놓은것 같아서 Decision Tree 이다.](/images/Decision_Tree/Decision_Tree-2.png) 

위의 그림에서 각각의 네모상자를 `노드`<sup>Node</sup>라고 하며, 가장 처음의 분기점을 `Root Node`라고 하고, 가장 마지막 노드를 `Leaf Node`또는 `Terminal Node`라고 한다.


### 결정나무분류기 = DecisionTreeClassifier

---
`DecisionTreeClassifier()`는 결정나무의 기능을 바꿀수 있는 파라미터인데 파라미터 내부의 특성 하나하나를 `하이퍼파라미터`라고 한다.  
<br>
`DecisionTreeClassifier()`파라미터의 괄호 안에 각각의 값을 입력할 수 있는데 다음과 같은 항목들이 있다.

|하이퍼파라미터|기능|
|:---:|:---:|
|criterion| 분할 품질을 측정하는 기능 (default : gini) |
|splitter|각 노드에서 분할을 선택하는 데 사용되는 전략 (default : best)|
|max_depth|트리의 최대 깊이 (값이 클수록 모델의 복잡도가 올라간다.)|
|min_samples_split|자식 노드를 분할하는데 필요한 최소 샘플 수 (default : 2)|
|min_samples_leaf|리프 노드에 있어야 할 최소 샘플 수 (default : 1)|
|min_weight_fraction_leaf|min_sample_leaf와 같지만 가중치가 부여된 샘플 수에서의 비율|
|max_features|각 노드에서 분할에 사용할 특징의 최대 수|
|random_state|난수 seed 설정|
|max_leaf_nodes|리프 노드의 최대수|
|min_impurity_decrease|최소 불순도|
|min_impurity_split|나무 성장을 멈추기 위한 임계치|
|class_weight|클래스 가중치|
|presort|데이터 정렬 필요 여부|

괄호 내부에 아무것도 입력하지않으면 기본값으로 결정나무가 출력된다.


# **References**


* [https://inuplace.tistory.com/548](https://inuplace.tistory.com/548)
* [https://scikit-learn.org/stable/modules/tree.html#classification](https://scikit-learn.org/stable/modules/tree.html#classification)