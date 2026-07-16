# WEEK 1 STUDY (2026.7.11-2026.7.14)

## 1-1 pakage
pass

## 1-2 framework & library
### 1. Tensorflow

머신러닝과 딥 러닝을 직관적으로 설계하게끔 도와준다.

관례 : tf로 import하는 것이 관례
```python
import tensorflow as tf
```

### 2. Keras

텐서플로우에대한 추상화된 API를 제공한다.
백엔드로 텐서플로우를 사용하고 더 쉽게 딥러닝을 사용할 수 있게해준다.

권장 사항 : 텐서플로우 내부의 keras를 사용하는 것을 권장하며 호출 방법은 tf.keras로 사용한다.

### 3. Gensim

토픽 모델링과 자연어 처리 등을 지원해주는 오픈 소스 라이브러리이다.

### 4. Scikit-learn

다양한 머신 러닝 모듈 또는 자체 데이터를 제공한다.


## 1-3 NLTK & KoNLPy

### 1. NLTK

자연어 처리를 위한 파이썬 패키지이다.
NLTK의 기능을 제대로 사용하려면 NLTK Data라는 데이터들을 추가적으로 설치해야한다.

### 2. KoNLPy

한국어 자연어 처리를 위한 형태소 분석기 패키지이다.


## 1-4 Pandas & Numpy & Matplotlib

### 1. Pandas

데이터 처리를 위한 라이브러리이다.

관례 : pd로 import하는 것이 관례
```python
import pandas as pd
```

- Series<br>
1차원 배열의 값에 각각 대응되는 인덱스를 부여하는 구조이다.
```python
sr = pd.Series(['hello','python','world','!'], index=['h','p','w','m'])

print(sr)
```
출력값
```
h     hello
p    python
w     world
m         !
dtype: object
```
시리즈는 List, Tuple, Dict로 생성할 수 있다.

- DataFrame<br>
2차원 리스트를 매개변수로 가진다.
행방향 인덱스와 열방향 인덱스가 존재한다.
```python
values = [[1,2,3],[4,5,6],[7,8,9]]
index = ['A','B','C']
columns = ['x','y','z']

df = pd.DataFrame(values, index=index, columns=columns)

print(df)
```
출력값
```
   x  y  z
A  1  2  3
B  4  5  6
C  7  8  9
```
데이터프레임은 List, Series, Dict, ndarrays 등으로 생성할 수 있다.

**데이터프레임 조회 명령어**
 - df.head(n) : 앞 부분을 n개 보기
 - df.tail(n) : 뒷 부분을 n개 보기
 - df['열이름']: 해당 열만 보기<br><br>


- Panel(not in book - investigate)<br>
현재는 삭제된 기능으로 3차원 데이터를 다루기위한 구조이다.
items, major_axis, minor_axis 이렇게 3개의 축으로 설계된다.

사라진 이유: 3차원 데이터의 수요 부족과 더 나은 대체 수단이 존재한다.

대체제: MultiIndex DataFrame, xarray

- 외부 데이터 읽기
pd.read_[파일 타입]('파일 명') 형태로 읽을 수 있다.
```python
#ex)
pd.read_csv('example.csv')
pd.read_json('example.json')
```

### 2. Numpy

수치 데이터를 다루는 패키지이다.
Numpy는 ndarray라고 불리는 행렬구조를 가지고있으며 벡터, 행렬 등의 여러 연산에서 사용된다.
ndarray는 n개의 dimension을 가지는 array라는 의미로 다중 차원 행렬을 보다 쉽게 계산할수있다는 장점이 있다.

관례 : np로 import하는 것이 관례
```python
import numpy as np
```

**numpy 명령어**
```
- np.array([1,2,3,4,5]): 입력값의 형태에따른 ndarray 생성
- np.zeros((n,m)): n*m크기의 모든 원소가 0인 ndarray 생성
- np.ones((n,m)): n*m크기의 모든 원소가 1인 ndarray 생성
- np.full((n,m), i): n*m크기의 모든 원소가 i인 ndarray 생성
- np.eye(n): n*n크기의 기준행렬 ndarray 생성
- np.random.random((n,n)): n*n크기의 모든 원소가 랜덤한 ndarray 생성
- np.arange(i, j, n): i부터 j-1까지 n만큼 증가하는 ndarray 생성

np.original_array.reshape((n,m)): original_array를 n*m크기의 ndarray로 변경
```

### 3. Matplotlib
데이터를 chart 또는 plot으로 시각화하기위해 사용하는 패키지이다.

관례 : plt로 import하는 것이 관례
```python
import matplotlib.pyplot as plt
```

## 1-5 Machine Learning Workflow

### 머신 러닝 워크플로우 과정
![image](./img/워크플로우%20과정.webp)

1. 수집
머신 러닝을 하기위해서는 학습시킬 데이터가 필요하다.
이때 자연어 처리에서는 이 데이터를 말뭉치 혹은 corpus라고 부른다.
>corpus: 조사나 연구 목적에 의해 특정 도메인으로부터 수집된 텍스트 집합

2. 점검 및 탐색
데이터의 구조, 노이즈 데이터, 머신 러닝 적용을 위해 데이터를 어떻게 정제하는가를 파악하는 단계이다.
이를 탐색적 데이터 분석 단계(EDA)라고하는데 변수의 데이터 타입등을 점검하며 데이터의 특징과 구조적 관계를 알아내는 과정을 뜻한다.

3. 전처리 및 정제
자연어 처리에서는 토큰화, 정제, 정규화, 불용어 제거 등의 단계를 포함하고 있다.

4. 모델링 및 훈련
적절한 머신 러닝 알고리즘을 선택하여 모델링을 한 후 데이터를 알고리즘을 통해 학습시킨다. 이를 training이라고 한다.

**주의점**
모든 데이터를 학습시키는 것이 아닌 테스트용 데이터를 남겨두어야한다. 그래야만 훈련용 데이터로 학습 후 테스트 데이터로 성능을 측정할 수 있고, 과적합을 방지할 수 있게된다.

5. 평가
테스트용 데이터로 성능을 평가하는 과정이다.
정답과 얼마나 가까운지 측정하게된다.

6. 배포
성공적으로 훈련되었다면 모델의 배포 과정을 거치게된다.
모델을 다시 업데이트해야한다면 수집단계로 돌아간다.