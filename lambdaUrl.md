# Lambda Functional URL


AWS의 대표적인 서비리스 서비스인 Lambda는 쉽게 생성하고 편리하게 쓸수 있으며, Concurrency도 제공하므로 편리하나, 외부에서 Lambda를 직접 호출 할 수 없었고, API Gateway를 거쳐야 했습니다. 소수로된 단순한 api를 private하게 사용하는 경우에 Lambda를 HTTPS 엔드포인트로 사용하면 매우 유용합니다. 

## Lambda Functional URL 이란?

[AWS Lambda 함수 URL](https://aws.amazon.com/ko/about-aws/whats-new/2022/04/aws-lambda-function-urls-built-in-https-endpoints/)이 2022년 4월에 상용 적용됨으로 인해, Lambda 함수를 외부에서 간단하게 접속 할 수 있습니다. 여기서는 Simple한 Data Acquisition Unit를 설계하므로, Lambda Functional URL 기능을 활용합니다. 




[Lambda for Functional URL](https://github.com/kyopark2014/simple-data-aquisition-unit/blob/main/lambda-for-functional-url.md)에 따라 Lambda를 생성하고, Functional URL 기능을 Enable 합니다. 

디바이스들로 부터 전달되는 이벤트는 application/json 방식의 Content-type을 가진다고 가정합니다. RESTful API를 통해 HTTPS POST를 이용해 데이터가 Lambda for Functional URL로 전달됩니다. 

## Lambda 함수 URL 보안


Lambda 함수 URL의 외부 접속을 제한하기 위해서는 AWS Identity and Access Management(IAM)을 사용하여야 합니다. 


![noname](https://user-images.githubusercontent.com/52392004/165218237-c78d26b7-1ce3-4bd4-ac63-b7ca8b71a37a.png)

