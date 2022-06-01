# Lambda 함수 URL과 Client 인증


## Lambda Functional URL 이란?

AWS의 대표적인 서비리스 서비스인 Lambda는 쉽게 생성하고 편리하게 쓸수 있으며, Concurrency도 제공하므로 편리하나, 외부에서 Lambda를 직접 호출 할 수 없었고, API Gateway를 포함하여야 합니다. API Gateway는 다양한 인증과 보안기능을 제공하나, 단 하나의 API를 간단히 구현하고자 하는 경우에도 API Gateway를 사용하여야 했습니다. 아래 그림은 일반적인 serverless architecture로서, DynamoDB를 조회하는 Lambda 함수를 위하여 API Gateway를 사용하고 있습니다. 

![image](https://user-images.githubusercontent.com/52392004/171417037-0d2f02a3-a09a-4e80-9ab5-5d993b2b9dc9.png)

[AWS Lambda 함수 URL](https://aws.amazon.com/ko/about-aws/whats-new/2022/04/aws-lambda-function-urls-built-in-https-endpoints/)이 2022년 4월에 상용 적용됨으로 인해, 단순한 api를 private하게 사용하는 경우에 Lambda를 HTTPS 엔드포인트로 사용하는 방법이 있습니다.

[Lambda 함수 URL 생성하기](https://github.com/kyopark2014/simple-data-aquisition-unit/blob/main/lambda-for-functional-url.md)에 따라 Lambda를 생성하고, Functional URL 기능을 Enable 할 수 있는데, 아래와 같은 Lambda 함수 URL을 간단하게 생성하여 사용 할 수 있습니다. 

![noname](https://user-images.githubusercontent.com/52392004/165218603-55d9c145-676e-4c40-a9f5-f46bb8a6d34f.png)

Lamdba 함수 URL은 아래와 같은 포맷으로 생성되는데, IPv4와 IPv6을 모두에서 https를 지원하고, cross-origin resource sharing (CORS)도 지원하고 있습니다. 

```c
https://<url-id>.lambda-url.<region>.on.aws
```

  
## Lambda 함수 URL 보안

Lambda 함수 URL은 인증 방식으로 AWS Identity and Access Management(IAM)만을 제공하므로, 외부 접속을 제한하기 위해서는 IAM을 사용하여야 합니다. 

![image](https://user-images.githubusercontent.com/52392004/171420558-e491ca84-b26e-43c5-af95-a1da86493bb9.png)

IAM은 



## Reference 
  
[Lambda function URLs](https://docs.aws.amazon.com/lambda/latest/dg/lambda-urls.html?icmpid=docs_lambda_help)
    
[Build a REST API with API Gateway, AWS Lambda, DynamoDB & AWS CDK](https://faun.pub/build-a-rest-api-with-api-gateway-aws-lambda-dynamodb-aws-cdk-616d1e17c128)
