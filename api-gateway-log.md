# API Gateway에서 로그 활용

API Gateway에서 로그를 Enable 하는 방법을 설명합니다.

1. [IAM console](https://console.aws.amazon.com/iamv2/home#/roles)에 접속합니다.
https://console.aws.amazon.com/iamv2/home#/roles

2. [Create roles]를 선택하고, 아래와 같이 [Use case]에서 "API Gateway"를 선태한 후에 [Next]를 선택합니다.

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/dc08efac-026b-4aa5-b120-0618a9d0188b)


3. 아래와 같이 "AmazonAPIGatewayPushToCloudWatchLogs"가 선택되어 있는것을 확인 후, [Next]를 선택합니다. 

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/2b8a528e-3b4d-4099-be74-f093f7e3b394)


4. 아래와 같이 [Role details]의 Role name에 적당한 이름을 넣습니다. 여기서는 "api-gateway-logs"로 입력하였고, 아래로 스크롤하여 [Create role]을 선택합니다.

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/666b8411-0b99-44c6-8a5a-f4b1ffb87b9e)

