# JSON 조작하는 방법


### Json 변수 출력하기 

아래처럼 json 데이터를 직접 입력받아서 json.dumps()을 통해 json object로 변환합니다. 두번째 케이스에서 indent는 들여쓰기 탭 갯수입니다. 

```python
jvalues = [{"fixed acidity":6.6,"volatile acidity":0.24,"citric acid":0.28,"residual sugar":1.8,"chlorides":0.028,"free sulfur dioxide":39.0,"total sulfur dioxide":132.0,"density":0.99182,"pH":3.34,"sulphates":0.46,"alcohol":11.4,"color_red":0,"color_white":1},{"fixed acidity":8.7,"volatile acidity":0.78,"citric acid":0.51,"residual sugar":1.7,"chlorides":0.415,"free sulfur dioxide":12.0,"total sulfur dioxide":66.0,"density":0.99623,"pH":3.0,"sulphates":1.17,"alcohol":9.2,"color_red":1,"color_white":0}]

values = json.dumps(jvalues)
print('values #1: ', values)

values = json.dumps(jvalues, ensure_ascii=False, indent=3)
print('values #2: ', values)
```

이때의 결과는 아래와 같습니다. 
```java
values #1:  [{"fixed acidity": 6.6, "volatile acidity": 0.24, "citric acid": 0.28, "residual sugar": 1.8, "chlorides": 0.028, "free sulfur dioxide": 39.0, "total sulfur dioxide": 132.0, "density": 0.99182, "pH": 3.34, "sulphates": 0.46, "alcohol": 11.4, "color_red": 0, "color_white": 1}, {"fixed acidity": 8.7, "volatile acidity": 0.78, "citric acid": 0.51, "residual sugar": 1.7, "chlorides": 0.415, "free sulfur dioxide": 12.0, "total sulfur dioxide": 66.0, "density": 0.99623, "pH": 3.0, "sulphates": 1.17, "alcohol": 9.2, "color_red": 1, "color_white": 0}]
values #2:  [
   {
      "fixed acidity": 6.6,
      "volatile acidity": 0.24,
      "citric acid": 0.28,
      "residual sugar": 1.8,
      "chlorides": 0.028,
      "free sulfur dioxide": 39.0,
      "total sulfur dioxide": 132.0,
      "density": 0.99182,
      "pH": 3.34,
      "sulphates": 0.46,
      "alcohol": 11.4,
      "color_red": 0,
      "color_white": 1
   },
   {
      "fixed acidity": 8.7,
      "volatile acidity": 0.78,
      "citric acid": 0.51,
      "residual sugar": 1.7,
      "chlorides": 0.415,
      "free sulfur dioxide": 12.0,
      "total sulfur dioxide": 66.0,
      "density": 0.99623,
      "pH": 3.0,
      "sulphates": 1.17,
      "alcohol": 9.2,
      "color_red": 1,
      "color_white": 0
   }
]
```

### Panda에서 읽은 후 Predict할 수 있는 Json 포맷으로 저장하기 

Panda를 이용해 읽은 데이터로 Predict를 하려면 "records" orient되어 있는 포맷이어야 합니다. Dataset에서 json 포맷으로 저장할 경우에 [xgboost-wine-quality-inference.ipynb](https://github.com/kyopark2014/ML-Algorithms/blob/main/kaggle/xgboost-wine-quality/xgboost-wine-quality-inference.ipynb)와 같이 저장합니다.

```python
X_test[:2].to_json('samples.json',orient='records')
```

상기와 같이하면, [samples.json](https://github.com/kyopark2014/ML-Algorithms/blob/main/kaggle/xgboost-wine-quality/samples.json)이 생성됩니다. 이 파일의 포맷은 아래와 같습니다. 

```java
[
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
      "color_red":0,
      "color_white":1
   }
]
```


### Json 파일 읽기

sample.json은 아래와 같습니다.

```java
[{"fixed acidity":6.6,"volatile acidity":0.24,"citric acid":0.28,"residual sugar":1.8,"chlorides":0.028,"free sulfur dioxide":39.0,"total sulfur dioxide":132.0,"density":0.99182,"pH":3.34,"sulphates":0.46,"alcohol":11.4,"color_red":0,"color_white":1},{"fixed acidity":8.7,"volatile acidity":0.78,"citric acid":0.51,"residual sugar":1.7,"chlorides":0.415,"free sulfur dioxide":12.0,"total sulfur dioxide":66.0,"density":0.99623,"pH":3.0,"sulphates":1.17,"alcohol":9.2,"color_red":1,"color_white":0}]
```

아래처럼 json파일을 읽습니다.

```java
json_file = pd.read_json('../data/samples.json')
print('file: ', json_file)
```

프린트한 결과는 아래와 같습니다. 
```java
file:     fixed acidity  volatile acidity  citric acid  residual sugar  chlorides  free sulfur dioxide  ...  density    pH  sulphates  alcohol  color_red  color_white
0            6.6              0.24         0.28             1.8      0.028                   39  ...  0.99182  3.34       0.46     11.4          0            1
1            8.7              0.78         0.51             1.7      0.415                   12  ...  0.99623  3.00       1.17      9.2          1            0
```


이렇게 읽은 Json 파일은 아래처럼 Machine Learning에서 predict 할때 사용할 수 있습니다. 

```python
records = pd.read_json('samples.json')
data = pd.DataFrame(records)

from xgboost import XGBRegressor
model = XGBRegressor()

model_name = "./output/xgboost_wine_quality.json"
model.load_model(model_name)

model.predict(data)
```

이때의 결과는 아래와 같습니다. 

```python
array([6.4810886, 4.7421913], dtype=float32)
```




### Trouble Shooting: "ValueError: Feature shape mismatch:

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


## json encoding/decoding

아래와 같은 json 데이터가 있습니다.

```java
data = {'body': '[{"fixed acidity":6.6,"volatile acidity":0.24,"citric acid":0.28,"residual sugar":1.8,"chlorides":0.028,"free sulfur dioxide":39,"total sulfur dioxide":132,"density":0.99182,"pH":3.34,"sulphates":0.46,"alcohol":11.4,"color_red":0,"color_white":1},{"fixed acidity":8.7,"volatile acidity":0.78,"citric acid":0.51,"residual sugar":1.7,"chlorides":0.415,"free sulfur dioxide":12,"total sulfur dioxide":66,"density":0.99623,"pH":3.0,"sulphates":1.17,"alcohol":9.2,"color_red":1,"color_white":0}]', 'isBase64Encoded': False}
```

전송등을 위해 dump를 이용해 encoding 합니다.

```java
data_dump = json.dumps(data)

{"body": "[{\"fixed acidity\":6.6,\"volatile acidity\":0.24,\"citric acid\":0.28,\"residual sugar\":1.8,\"chlorides\":0.028,\"free sulfur dioxide\":39,\"total sulfur dioxide\":132,\"density\":0.99182,\"pH\":3.34,\"sulphates\":0.46,\"alcohol\":11.4,\"color_red\":0,\"color_white\":1},{\"fixed acidity\":8.7,\"volatile acidity\":0.78,\"citric acid\":0.51,\"residual sugar\":1.7,\"chlorides\":0.415,\"free sulfur dioxide\":12,\"total sulfur dioxide\":66,\"density\":0.99623,\"pH\":3.0,\"sulphates\":1.17,\"alcohol\":9.2,\"color_red\":1,\"color_white\":0}]", "isBase64Encoded": false}
```

실제 사용을 위해 다시 아래처럼 decoding하여 사용합니다.
```java
json_data = json.loads(data)

{'body': '[{"fixed acidity":6.6,"volatile acidity":0.24,"citric acid":0.28,"residual sugar":1.8,"chlorides":0.028,"free sulfur dioxide":39,"total sulfur dioxide":132,"density":0.99182,"pH":3.34,"sulphates":0.46,"alcohol":11.4,"color_red":0,"color_white":1},{"fixed acidity":8.7,"volatile acidity":0.78,"citric acid":0.51,"residual sugar":1.7,"chlorides":0.415,"free sulfur dioxide":12,"total sulfur dioxide":66,"density":0.99623,"pH":3.0,"sulphates":1.17,"alcohol":9.2,"color_red":1,"color_white":0}]', 'isBase64Encoded': False}
```

## Reference 

[[Pandas] JSON 읽고 DataFrame으로 상호 변환하기](https://bio-info.tistory.com/113)

[pandas read_json: "If using all scalar values, you must pass an index"](https://stackoverflow.com/questions/38380795/pandas-read-json-if-using-all-scalar-values-you-must-pass-an-index)
