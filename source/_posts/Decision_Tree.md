---
title: 결정 나무(Decision Tree)
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

  
### 결정나무의 의사결정 과정

---

결정 나무가 행하는 이 과정은 '스무고개'를 할때의 그것과 비슷하다.  
사과, 포도, 멜론, 녹차를 구분한다고 생각해보자. 사과와 포도는 과일이고 멜론과 녹차는 과일이 아니다.  
'과일인가요?'라는 질문을 통해 사과, 포도 / 멜론, 녹차를 나눌 수 있고, 사과와 포도는 '(과실 전체의)모양이 둥근가요?', 멜론과 녹차는 '넝쿨에서 자라나요?' 라는 질문을 통해 분류해 낼 수 있다.  
위의 결정나무를 도식화하면 아래와 같다.

![도식화한 결정나무](/images/Decision_Tree/Decision_Tree-1.png)  
  
이렇게 질문에 따라 데이터를 구분짓는 모델을 `결정나무`모델이라고 한다. 한번의 질문에 True 혹은 False를 통해 변수영역을 두 개로 분기한다.  
위의 그림에서 각각의 네모상자를 `노드`<sup>Node</sup>라고 하며, 가장 처음의 분기점을 `Root Node`라고 하고, 가장 마지막 노드를 `Leaf Node`또는 `Terminal Node`라고 한다.

![모양이 나무를 뒤집어 놓은것 같아서 Decision Tree 이다.](/images/Decision_Tree/Decision_Tree-2.png) 

### 결정나무의 기본적인 형태

---

```python
from sklearn import tree # sklearn 모듈로부터 tree를 import

X = [[0, 0], [1, 1]] # 데이터셋 생성               
Y = [0, 1]

clf = tree.DecisionTreeClassifier() 
clf = clf.fit(X, Y)
clf.predict([[1, 1]])
```
<details> 
<summary>Output</summary>

    array([1])

</details>

