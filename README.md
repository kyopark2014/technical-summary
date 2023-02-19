# 기술 문서 

기술적으로 정리한 문서를 여기에 공유하고자 합니다. 

## [CDK 소개](https://github.com/kyopark2014/techinical-summary/blob/main/cdk-introduction.md)

CDK는 무엇인지와 장점등에 대해 설명합니다. 

## [CDK Reference](https://github.com/kyopark2014/techinical-summary/blob/main/cdk-reference.md) 

CDK 관련 typescript reference를 정리합니다. 

## [Kinesis Data Stream](https://github.com/kyopark2014/technical-summary/blob/main/kinesis-data-stream.md)

Kinesis Data Stream에 대해 설명하고, Kafka와 비교합니다. 

## [Kinesis Data Firehose](https://github.com/kyopark2014/technical-summary/blob/main/kinesis-data-firehose.md)

Kinesis Data Firehose의 주요 기능에 대해 설명합니다.


## [SQS](https://github.com/kyopark2014/technical-summary/blob/main/sqs.md)

Amazon SQS에 사양에 대해 설명합니다. 


## [Call Center Analytics](https://github.com/kyopark2014/technical-summary/blob/main/call-center-analytics.md)

Call Center 솔루션인 AWS Connect에서 모아진 CTR 데이터를 수집하는 Architecture에 대해 설명합니다. 

## [Slack Token 발급](https://github.com/kyopark2014/serverless-storytime/blob/main/docs/slackapp.md)

Slack으로 메시지를 보내기 위한 Token 생성 및 업데이트에 대해 설명합니다. 

## [Node Reference](https://github.com/kyopark2014/technical-summary/blob/main/node-reference.md)

Node.js 관련 레퍼런스를 정리합니다. 

## [유용한 명령어](https://github.com/kyopark2014/technical-summary/blob/main/useful-commands.md)

유용한 명령어들을 정리합니다. 


## [Canary deployment in API Gateway](https://github.com/kyopark2014/technical-summary/blob/main/canary-api-gateway.md)

API Gateway에서 Canary Deployment 하는 방법을 설명합니다.


## ML을 위하여 Json 파일로 저장하고 읽어서 활용하기

[json-manupulation.md](https://github.com/kyopark2014/technical-summary/blob/main/json-manupulation.md) Panda를 이용하여 ML을 위한 Json 파일의 저장 및 읽는 방법에 대해 설명합니다. 


## Cloud9 resize

[resize.md](https://github.com/kyopark2014/technical-summary/blob/main/resize.md)에서는 Cloud9에서 EBS 크기 변경에 대해 설명합니다.



## NLB (Network Load Balancer) Limitation

[Connection idle timeout](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/network-load-balancers.html)




For each TCP request that a client makes through a Network Load Balancer, the state of that connection is tracked. If no data is sent through the connection by either the client or target for longer than the idle timeout, the connection is closed. If a client or a target sends data after the idle timeout period elapses, it receives a TCP RST packet to indicate that the connection is no longer valid.

Elastic Load Balancing sets the **idle timeout value for TCP flows to 350 seconds**. You cannot modify this value. Clients or targets can use TCP keepalive packets to reset the idle timeout. Keepalive packets sent to maintain TLS connections cannot contain data or payload.

While UDP is connectionless, the load balancer maintains UDP flow state based on the source and destination IP addresses and ports, ensuring that packets that belong to the same flow are consistently sent to the same target. After the idle timeout period elapses, the load balancer considers the incoming UDP packet as a new flow and routes it to a new target. Elastic Load Balancing sets the idle timeout value for UDP flows to 120 seconds.

EC2 instances must respond to a new request within 30 seconds in order to establish a return path.

## ETC

[Python으로 Lambda 생성후 Request 하기](https://github.com/kyopark2014/technical-summary/blob/main/lambda-python.md)

[Github 파일을 링크로 걸기](https://github.com/kyopark2014/technical-summary/blob/main/github-raw-file.md)
