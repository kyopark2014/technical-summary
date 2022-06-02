# Lambda 함수 URL을 이용하여 편리하고 안전하게 API 서버와 클라이언트 만들기


## Lambda 함수 URL 이란?

AWS의 대표적인 서비리스 서비스인 Lambda는 인프라에 대한 고민없이 개발에만 집중할 수 있어 편리하며, Concurrency에 기반한 오토 스케일링으로 부하의 변동에 쉽게 대응할 수 있으며, 사용하지 않을 경우에는 비용이 발생하지 않아서 경제적입니다. 하지만 그동안 외부에서 Lambda를 직접 호출 할 수 없어, API Gateway를 Endpoint로 사용하여야 했습니다. API Gateway는 다양한 인증과 편리한 기능을 제공하나, 하나 또는 소수의 API를 간단히 구현하여 Private하게 사용하는 경우에도 API Gateway를 사용하여야 했습니다. 아래 그림은 [일반적인 serverless architecture](https://faun.pub/build-a-rest-api-with-api-gateway-aws-lambda-dynamodb-aws-cdk-616d1e17c128)로서, DynamoDB를 조회하는 Lambda 함수를 위하여 API Gateway를 사용하고 있습니다. 

![image](https://user-images.githubusercontent.com/52392004/171417037-0d2f02a3-a09a-4e80-9ab5-5d993b2b9dc9.png)

[AWS Lambda 함수 URL](https://aws.amazon.com/ko/about-aws/whats-new/2022/04/aws-lambda-function-urls-built-in-https-endpoints/)이 2022년 4월에 상용 적용됨으로 인해, API Gateway없이 Lambda를 HTTPS 엔드포인트로 사용할 수 있게 되었습니다. 아래 그림은 Lambda 함수 URL을 통해 DynamoDB를 조회하는 Architecture를 보여줍니다. 여기서, API Gateway 없이 Lambda로 직접 접속할 수 있어서 간단하고 편리하게 API를 제공 할 수 있습니다. 

![image](https://user-images.githubusercontent.com/52392004/171504682-3599dbdf-3043-4657-9cf0-fceab7901a42.png)

  
## Lambda 함수 URL 생성하기

[Lambda 함수 URL 설정](https://github.com/kyopark2014/simple-data-aquisition-unit/blob/main/lambda-for-functional-url.md)에 따라 Lambda 함수 URL 기능을 Enable 할 수 있습니다.

Lambda 함수 URL을 Enable한 후, 아래와 같이 htts endpoint로 사용할 수 있는 URL을 알 수 있습니다.

![noname](https://user-images.githubusercontent.com/52392004/165218603-55d9c145-676e-4c40-a9f5-f46bb8a6d34f.png)

Lamdba 함수 URL은 아래와 같은 포맷이며, IPv4와 IPv6을 모두에서 https를 지원하고, cross-origin resource sharing (CORS)도 지원하고 있습니다. 

```c
https://<url-id>.lambda-url.<region>.on.aws
```


## Lambda 함수 URL 보안

Lambda 함수 URL은 인증 방식으로 AWS Identity and Access Management(IAM)만을 제공하므로, 외부 접속을 제한하기 위해서는 IAM을 사용하여야 합니다. 

![image](https://user-images.githubusercontent.com/52392004/171420558-e491ca84-b26e-43c5-af95-a1da86493bb9.png)

IAM Credential은 AccessKeyId와 SecretAccessKey으로 구성되는데, 외부에 공개되지 않도록 세심한 주의가 필요합니다. 따라서, client에서 IAM Credential을 직접 사용하기 보다는 temparary security credential을 생성하여 사용하는것이 바람직합니다. Temporary security credentials의 expire time을 설정하면, 수분에서 수시간까지 변경 할 수 있으며, 시간이 만료되면 더이상 사용할 수 없습니다. 

Temporary security credentials은 STS(Security Token Server)을 통해 획득하는데, resource-based policies를 따르므로 [Lambda를 이용한 STS 연결](https://github.com/kyopark2014/aws-security-token-service/tree/main/lambda-for-sts)과 같이 AWS SDK를 이용해 생성할 수 있습니다. 



## Temperary Security Credential로 Lambda 함수 URL을 호출하는 Client 만들기 

[Temparary security credential 을 이용하여 Lambda Function URL 접속](https://github.com/kyopark2014/aws-security-token-service/blob/main/lambda-invation-using-temp-credential.md)에서는 Temperary security credential을 이용하여 Postman을 통해 Lambda 함수 URL에 접속하는 방법을 설명하고 있습니다. 하지만, 이러한 방법으로 Postman에 매번 Temparary security credential을 생성하여 넣는 것은 매우 번거로우므로, Client 직접 Temperary security credential을 생성하고 request를 보낼 수 있어야 합니다. 이것은 [Signing AWS requests with Signature Version 4](https://docs.aws.amazon.com/general/latest/gr/sigv4_signing.html)을 이용하여 [Crypto로 직접 인증을 수행](https://github.com/kyopark2014/aws-security-token-service/tree/main/lambda-for-authentification-request-using-crypto)하거나, AWS SDK를 통해 구현이 가능합니다. 아래에서는 AWS SDK를 이용해서 temparary security credential을 생성하고, 이를 이용해 request를 singing하는 과정을 설명합니다. 

#### AWS SDK를 이용하여 temparary security credential 생성

기 생성한 Role을 가지고 아래와 같이 STS를 통해 Temperary security credential을 생성합니다.

```java
   const params = {
        RoleArn: 'arn:aws:iam::123456789012:role/role-for-s3-fileserver',
        RoleSessionName: 'session',
    };
    const assumeRoleCommand = new AssumeRoleCommand(params);
    
    let data;
    try {
        data = await sTS.send(assumeRoleCommand);
    
        console.log('data: %j',data);
    } catch (error) {
          console.log(error);
    }
```

새로운 credential로 AWS의 Config를 업데이트 합니다.

```java
    aws.config.credentials.accessKeyId = data.Credentials.AccessKeyId;
    aws.config.credentials.sessionToken = data.Credentials.SessionToken;
    console.log("modified credentials: %j", aws.config.credentials);
```

#### signed된 request 생성 

아래와 같이 signature를 구합니다.

```java
    var region = 'ap-northeast-2';
    var domain = 'hgwavninyisqd6utbvywn7drpe0mvkwp.lambda-url.ap-northeast-2.on.aws';
    
    console.log('domain: '+domain);

    var myService = 'lambda';
    var myMethod = 'GET';
    var myPath = '/';
    var body = '';

    // Create the HTTP request
    var request = new HttpRequest({
        headers: {
            'host': domain
        },
        hostname: domain,
        method: myMethod,
        path: myPath,
        body: body,
    });
    console.log('request: %j', request);

    // Sign the request
    var signer = new SignatureV4({
        credentials: defaultProvider(),
        region: region,
        service: myService,
        sha256: Sha256
    });
    console.log('signer: %j', signer);

    var signedRequest;
    try {
        signedRequest = await signer.sign(request);
        console.log('signedRequest: %j', signedRequest);

    } catch(err) {
        console.log(err);
    }
```

아래와 같이 https로 Lambda Function URL에 접속을 합니다.

```java
    // request
    performRequest(domain, signedRequest.headers, signedRequest.body, myPath, myMethod, function(response) {    
        console.log('response: %j', response);
    });
    
    
// the REST API call using the Node.js 'https' module
function performRequest(endpoint, headers, data, path, method, success) {
    var dataString = data;
  
    var options = {
      host: endpoint,
      port: 443,
      path: path,
      method: method,
      headers: headers
    };

    var req = https.request(options, function(res) {
        res.setEncoding('utf-8');
    
        var responseString = '';
    
        res.on('data', function(data) {
            responseString += data;
        });
    
        res.on('end', function() {
            //console.log(responseString);
            success(responseString);
        });
    });

    req.write(dataString);
    req.end();
} 
```

상세한 코드는 [github code](https://github.com/kyopark2014/aws-security-token-service/blob/main/client/client-url.js)를 참조합니다.

아래와 같이 client를 node로 실행합니다.

$ node client-url.js

## Reference 
  
[Lambda function URLs](https://docs.aws.amazon.com/lambda/latest/dg/lambda-urls.html?icmpid=docs_lambda_help)
    
[Build a REST API with API Gateway, AWS Lambda, DynamoDB & AWS CDK](https://faun.pub/build-a-rest-api-with-api-gateway-aws-lambda-dynamodb-aws-cdk-616d1e17c128)

[AWS STS를 이용한 Temparary security credential 활용하기](https://github.com/kyopark2014/aws-security-token-service)

[AWS Lambda Function URL 발표 – 단일 기능 마이크로서비스용 내장 HTTPS 엔드포인트(Alex Casalboni)](https://aws.amazon.com/ko/blogs/korea/announcing-aws-lambda-function-urls-built-in-https-endpoints-for-single-function-microservices/)

[AWS Lambda: function URL is live!](https://lumigo.io/blog/aws-lambda-function-url-is-live/)
