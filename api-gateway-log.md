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

생성된 API Gateway Role의 ARN은 아래와 같습니다.

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/f0ef9e8b-144f-4c96-a102-cf35c9fe9778)


5. [API Gateway console - Settings](https://ap-northeast-2.console.aws.amazon.com/apigateway/main/settings?api=unselected&region=ap-northeast-2)에서 [Edit]를 선택한 후에 아래와 같이 생성한 IAM Role의 ARN을 [CloudWatch log role ARN]에 입력합니다.

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/fed44470-8209-4c54-b2de-b0018bbaa257)

6. [API Gateway Console](https://ap-northeast-2.console.aws.amazon.com/apigateway/main/apis?region=ap-northeast-2)에서 아래와 같이 아래와 같이 로그를 수집할 API Gateway를 선택합니다. 

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/ed9c5583-d0ef-45de-9939-63b3f836ac4c)

7. 아래와 같이 [Stages]를 선택하고 오른쪽 [Logs and tracing]에서 [Edit]를 선택합니다. 

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/71ed8420-5c69-4954-936e-dfa2704fa218)

8. [CloudWatch logs]에서 아래와 같이 "Detailed metrics"을 선택하고, [Save changes]를 선택합니다.

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/e32edeae-ade2-44c2-acc3-6f6c3b28403f)

9. CloudWatch의 [All metrics] - [Browse]에서 로그에 "API Gateway"를 선택합니다.
    
![image](https://github.com/kyopark2014/technical-summary/assets/52392004/f6cf9dc5-804e-4ff2-93df-c0d14c467e3a)

10. 이후 아래와 같이 "By Method"를 선택합니다.

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/ec40cef0-f24f-4dfe-871d-b8dca6dd9c22)

11. 아래와 같이 리소스 별로 metric을 확인할 수 있습니다.

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/6ee5f27f-01a0-4c66-b014-7bdbacc7aa55)

12. metric중에 '/provisioning'에 대한 호출수를 count하고 싶다면 아래와 같이 선택합니다.

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/16d1f01b-c12d-42f0-ac1d-ac628486ef92)

    
