# Python으로 Lambda 생성후 Request 하기

## Console에서 Python으로 생성된 Lambda 배포하기 

requests 라이브러리 설치는 아래와 같이 수행합니다.

```java
pip install \
    --target=lambda \
    requests
```

압축후 Console에서 zip으로 업로드 합니다. 압축시 lambda 소스 폴더를 포함하여 압축하여야 합니다. 

```java
cd lambda
zip -r lambda.zip .
```

lambda_function.py의 내용은 아래와 같습니다. 

```java
import json
import requests

def lambda_handler(event, context):
    #body = event['body']
    
    #txt = body['text']
    
    data = {
        "predictions":[{
            "prompt": "astronaut on a horse",
            "width": 768,
            "height": 768,
            "num_images_per_prompt": 1,
            "num_inference_steps": 50,
            "guidance_scale": 7.5
        }]
    }

    URL = 'https://runtime.sagemaker.ap-northeast-2.amazonaws.com/endpoints/jumpstart-example-infer-model-txt2img-s-2023-02-06-15-08-09-213/invocations'
    response = requests.post(URL, data=data)
    
    print(response.status_code)
    print(response.text)
        
    # TODO implement
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }
```

## Reference 

[컴파일된 바이너리가 포함된 Python 패키지를 배포 패키지에 추가하고 패키지를 Lambda와 호환되게 하려면 어떻게 해야 하나요?](https://aws.amazon.com/ko/premiumsupport/knowledge-center/lambda-python-package-compatible/)
