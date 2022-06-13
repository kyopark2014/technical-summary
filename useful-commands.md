## 유용한 명령어들 

### Account id 확인 방법 

```c
$ aws sts get-caller-identity --query Account --output text
```

### JSON 특정 변수 가져와서 사용하기 

config.json의 예제입니다. 

```java
{
    "Artifacts": {
        "S3Bucket": "greengrass-ml-inference-workshop",
        "S3Prefix": "ggv2/artifacts",
        "ZipArchiveName": "my-model"
    },
}
```

S3Bucket 이름 가져오는 방법입니다. 

```
$ cat config.json | jq -r '.Artifacts.S3Bucket'
greengrass-ml-inference-workshop
```

shell script에서 이를 활용하는 방법은 아래와 같습니다. 

```java

sudo yum install jq -y
jq --version

S3_BUCKET=$(cat config.json | jq -r '.Artifacts.S3Bucket')
S3_PREFIX=$(cat config.json | jq -r '.Artifacts.S3Prefix')

S3_PATH="s3://${S3_BUCKET}/${S3_PREFIX}"

echo s3 path: $S3_PATH
```

