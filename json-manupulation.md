# JSON 조작하는 방법

## jupyter noterbook

### 일반적인 Json을 읽는 경우 

아래와 같은 일반적인 json 형태로 저장하면 ML의 predict에서 사용하지 못합니다. 

sample.json

```java
{
    "fixed acidity":6.6,
    "volatile acidity":0.24,
    "citric acid":0.28,
    "residual sugar":1.8,
    "chlorides":0.028,
    "free sulfur dioxide":39.0,
    "total sulfur dioxide":132.0,
    "density":0.99182,
    "pH":3.34,
    "sulphates":0.46,
    "alcohol":11.4,
    "color_red":0.0,
    "color_white":1.0
 }
```

이것을 아래처럼 읽으면 "ValueError: If using all scalar values, you must pass an index"에러로 수행할수 없습니다.
```python
js = pd.read_json('sample.json')
```

따라서, 아래와 같이 읽을 수 있습니다.

```python
js = pd.read_json('sample.json', typ='dictionary')
data = pd.DataFrame(js)
data
```

이때의 결과는 아래와 같습니다.

![image](https://user-images.githubusercontent.com/52392004/199205986-8fc6473c-3200-4387-8209-41934f801844.png)

이것을 아래와 같이 predict하면 "ValueError: Feature shape mismatch, expected: 13, got 1" 에러가 발생합니다. 

![image](https://user-images.githubusercontent.com/52392004/199206243-cd29217a-5967-44dd-92be-5b5f73cf51aa.png)


### Panda에서 읽은 후 Predict가 가능한 포맷





## Reference 

[[Pandas] JSON 읽고 DataFrame으로 상호 변환하기](https://bio-info.tistory.com/113)

[pandas read_json: "If using all scalar values, you must pass an index"](https://stackoverflow.com/questions/38380795/pandas-read-json-if-using-all-scalar-values-you-must-pass-an-index)
