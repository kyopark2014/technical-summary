# Lambda Functional URL

## Lambda Functional URL 이란?

[AWS Lambda Functional URLs](https://aws.amazon.com/ko/about-aws/whats-new/2022/04/aws-lambda-function-urls-built-in-https-endpoints/)이 2022년 4월에 상용 적용됨으로 인해, Lambda 함수를 외부에서 간단하게 접속 할 수 있습니다. 여기서는 Simple한 Data Acquisition Unit를 설계하므로, Lambda Functional URL 기능을 활용합니다. 

[Lambda for Functional URL](https://github.com/kyopark2014/simple-data-aquisition-unit/blob/main/lambda-for-functional-url.md)에 따라 Lambda를 생성하고, Functional URL 기능을 Enable 합니다. 

디바이스들로 부터 전달되는 이벤트는 application/json 방식의 Content-type을 가진다고 가정합니다. RESTful API를 통해 HTTPS POST를 이용해 데이터가 Lambda for Functional URL로 전달됩니다. 
