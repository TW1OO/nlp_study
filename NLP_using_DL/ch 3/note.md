# WEEK 3 STUDY (2026.8.6-????.??.??)

## 3-1 What is Language Model?
언어 모델을 만드는 방법은 **통계를 이용한 방법**과 **인공 신경망을 이용한 방법**으로 구분할 수 있다.
최근에는 인공 신경망을 이용한 밥법이 더 좋은 성능을 보이며 트렌드라고 할 수 있다.

### 1. Language Model
언어 모델이란 단어 시퀀스에 확률을 할당(assign)하는 모델을 말한다.
더 쉽게 표현하면, 가장 자연스러운 단어 시퀀스를 찾아내는 모델이다.
이 단어 시퀀스를 찾아내는 방법은 주로 이전 단어가 주어졌을때 다음 단어를 예측하는 방법을 사용한다.

또 다른 방법으로는 주어진 양쪽 단어들로 가운데 비어있는 단어를 예측하는 모델이 있다. 고등학교 시험의 빈칸 추론 문제와 비슷한 문맥이다.

언어 모델에 -ing를 붙인 Language Modeling은 주어진 단어들에서 아직 모르는 단어를 예측하는 작업을 뜻한다. 이는 이전 단어들로 다음 단어를 예측한다는 의미이다.
자연어 처리로 유명한 스탠포드 대학에서는 언어 모델을 문법(grammar)으로 비유하기도 한다. 언어 모델이 단어의 조합이 얼마나 적절한지, 해당 문장이 얼마나 적합한지를 알려주는 일이 문법이 하는 일과 비슷하기때문이다.

### 2. 단어 시퀀스의 확률 할당
*P = Probability*

- a. Machine Translation
```
P(나는 버스를 탔다) > P(나는 버스를 태운다)
```
: 언어 모델은 두 문장을 비교해서 좌측의 문장 확률이 더 높다고 판단한다.

- b. Spell Correction
```
선생님이 교실로 부리나케
P(달려갔다) > P(잘려갔다)
```
: 언어 모델은 두 문장을 비교해서 좌측의 문장 확률이 더 높다고 판단한다.

- c. Speech Recognition
```
P(나는 메롱을 먹는다) < P(나는 메론을 먹는다)
```
: 언어 모델은 두 문장을 비교하여 오른쪽 문장의 확률이 더 높다고 판단한다.
언어 모델은 위와 같이 확률을 통해서 보다 적절한 문장을 파악한다.

### 3. 주어진 단어들로부터 단어 예측

- a. 단어 시퀀스의 확률  
w = 하나의 단어, W = 단어 시퀀스  
n개의 단어가 등장하는 단어 시퀀스 W의 확률
$$P(W) = P(w_1, w_2, w_3, w_4, w_5, \ldots, w_n)$$
- b. 다음 단어 등장 확률
n-1개의 단어가 나열되어있을때 n번째 단어의 확률
$$P(w_n \mid w_1, \ldots, w_{n-1})$$

전체 단어 시퀀스의 확률  
$$P(W) = P(w_1, w_2, w_3, w_4, w_5, \ldots, w_n) = \prod_{i=1}^{n}P(w_{i} \mid w_{1}, \ldots, w_{i-1})$$

### 4. 언어 모델의 간단한 직관
사람은 '비행기를 타려고 공항에 갔는데 지각을 하는 바람에 비행기를 [?]'라는 문장이 있을때 '비행기를' 다음에 '놓쳤다'라는 단어가 나올 것이라고 예상할 수 있다.


## 3-2 Statistical Language Model

### 1. 조건부 확률
조건부 확률 관계  
  
$$P(B|A) = P(A,B) / P(A)$$
$$P(A,B) = P(A)P(B|A)$$
  
조건부 확률의 연쇄 법칙  
  
$$P(A,B,C,D) = P(A)P(B|A)P(C|A,B)P(D|A,B,C)$$
  
n개 확률의 연쇄 법칙  
$$P(x_1, x_2, x_3 ... x_n) = P(x_1)P(x_2|x_1)P(x_3|x_1,x_2)...P(x_n|x_1 ... x_{n-1})$$

### 2. 문장에 대한 확률
예시 문장 'An adorabble little boy is spreading smiles'를 식으로 표현하면 $$P(An adorabble little boy is spreading smiles)$$로 표현할 수 있다.  
  
각 단어는 문맥이라는 관계로 인해 이전 단어의 영향을 받아 나온다. 그리고 이러한 모든 단어들로 하나의 문장이 완성된다.  
그렇기때문에 문장의 확률을 구할때 조건부 확률을 사용할 수 있다.  
$$P(w_1, w_2, w_3, w_4, w_5, ... w_n) = \prod_{n=1}^{n}P(w_{n} | w_{1}, ... , w_{n-1})$$
  
위 수식을 적용하면 다음과 같다.
$$P(\text{An adorable little boy is spreading smiles}) = P(\text{An})  ×  P(\text{adorable|An})  ×  P(\text{little|An adorable})  ×  P(\text{boy|An adorable little})  ×  P(\text{is|An adorable little boy})$$

### 3. 카운트 기반의 접근
SLM은 이전 단어로부터 다음 단어의 확률을 구할때 카운트에 기반하여 확률을 계산한다.  
$$P(\text{is|An adorable little boy}) = \frac{\text{count(An adorable little boy is)}}{\text{count(An adorable little boy )}}$$
그 확률은 위와 같다.  
만약 학습한 코퍼스 데이터에서 An adorable little boy가 100번 등장했을때 그 다음에 is가 등장한 경우는 30번이라고 하면
$P(\text{is|An adorable little boy})$는 30%이다
  
### 4. 희소 문제(카운트 기반 접근의 한계)
$$P\text{(is|An adorable little boy}) = \frac{\text{count(An adorable little boy is})}{\text{count(An adorable little boy })}$$
위와 같이 $P\text{(is|An adorable little boy})$를 구하는 경우에 기계가 훈련한 코퍼스에 An adorable little boy is라는 단어 시퀀스가 없다면 이 단어 시퀀스의 확률은 0이 된다.  
또는 An adorable little boy라는 단어 시퀀스가 없다면 분모가 0이 되어 확률은 정의되지않는다.  
이와 같이 충분한 데이터를 관측하지 못해 언어를 정확히 모델링하지 못하는 문제를 희소 문제(sparsity problem)라 한다.  
위 문제를 완화하기위해 n-gram 언어 모델과같은 여러 generalization 기법들이 존재하지만 희소 문제의 근본적인 해결책이 되지못하였다.  
  
## 3-3 N-gram Language Model
n-gram 언어 모델이란 모든 단어를 고려하는 것이 아니라 일부 단어만 고려하는 접근 방법을 사용하는 모델이다. 이때 일부 단어의 개수를 결정하는데 이것이 n의 의미이다.  
  
### 1. 코퍼스에서 카운트하지 못하는 경우의 감소
SLM은 훈련 코퍼스에 확률을 계산하고자하는 문장이나 단어가 없을 수 있다는 한계를 가진다. 그리고 문장이 길어질수록 존재하지않을 가능성은 더 높아진다. 즉, 카운트하지 못할 가능성이 높다. 그러나 참고하는 단어를 줄이면 카운트할 가능성을 높일 수 있다.  
$$P(\text{is|An adorable little boy}) \approx\ P(\text{is|boy})$$
$$P(\text{is|An adorable little boy}) \approx\ P(\text{is|little boy})$$
An adorable little boy가 나왔을 때 is가 나올 확률을 그냥 boy가 나왔을 때 is가 나올 확률로 생각해보면 boy is라는 단어 시퀀스가 존재할 가능성이 더 높을 것이다. 혹은 little boy가 나왔을 때 is가 나올 확률로 생각하는 것도 가능할 것이다.  
  
즉, 원래는 'An adorable little boy'가 나왔을 때 'is'가 나올 확률을 구하기 위해서는 'An adorable little boy'가 나온 횟수와 'An adorable little boy is'가 나온 횟수를 카운트해야했지만, 위 방식을 사용하면 단어의 확률을 구하기위해 기준 단어의 앞을 전부 카운트할 필요없이, 앞 단어 중 임의의 개수만 포함해서 근사치를 구하게된다.  
  
### 2. N-gram
