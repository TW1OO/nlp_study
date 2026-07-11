#WEEK 1 STUDY (2026.7.11-????)

##1-1 pakage
pass

##1-2 framework & library

1. Tensorflow

머신러닝과 딥 러닝을 직관적으로 설계하게끔 도와준다.

관례 : tf로 import하는 것이 관례
```python
import tensorflow as tf
```

2. Keras

텐서플로우에대한 추상화된 API를 제공한다.
백엔드로 텐서플로우를 사용하고 더 쉽게 딥러닝을 사용할 수 있게해준다.

권장 사항 : 텐서플로우 내부의 keras를 사용하는 것을 권장하며 호출 방법은 tf.keras로 사용한다.

3. Gensim

토픽 모델링과 자연어 처리 등을 지원해주는 오픈 소스 라이브러리이다.

4. Scikit-learn

다양한 머신 러닝 모듈 또는 자체 데이터를 제공한다.


##1-3 NLTK & KoNLPy

1. NLTK

자연어 처리를 위한 파이썬 패키지이다.
NLTK의 기능을 제대로 사용하려면 NLTK Data라는 데이터들을 추가적으로 설치해야한다.

2. KoNLPy

한국어 자연어 처리를 위한 형태소 분석기 패키지이다.

##1-4 Pandas & Numpy & Matplotlib

1. Pandas

데이터 처리를 위한 라이브러리이다.

관례 : pd로 import하는 것이 관례
```python
import pandas as pd
```

- Series
1차원 배열의 값에 각각 대응되는 인덱스를 부여하는 구조
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

- DataFrame
- Panel