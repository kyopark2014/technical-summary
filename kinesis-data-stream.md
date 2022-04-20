# Kinesis Data Stream 이란?

## 정의

Amazon Kinesis Data Streams is a serverless streaming data service that makes it easy to capture, process, and store data streams at any scale.

<img width="804" alt="image" src="https://user-images.githubusercontent.com/52392004/164144874-3337a267-03fa-469b-a53e-4410e9de6469.png">

## 사용 케이스 

1) Steam log and event data: Ingest and collect terabytes of data per day from application and service logs, clickstream data, sensor data, and in-app user events to power live dashboards, generate metrics, and deliver data into data lakes.

2) Run real-time analytics: Build applications for high-frequency event data such as clickstream data, and gain access to insights in seconds, not days, using AWS Lambda or Amazon Kinesis Data Analytics.

3) Power event-driven applications: Quickly pair with AWS Lambda to respond to or adjust immediate occurrences within the event-driven applications in your environment, at any scale.


## Benefits of Stream storage

![image](https://user-images.githubusercontent.com/52392004/164147360-3f405d67-f62d-42c2-bced-870fae479ac0.png)


## Kafka 비교 

<img width="1168" alt="image" src="https://user-images.githubusercontent.com/52392004/164147507-51be8eb7-9d09-4a2e-933d-2f62254b8e14.png">

PK: Partition Key

<img width="1115" alt="image" src="https://user-images.githubusercontent.com/52392004/164147535-a960b91c-7b59-4b91-9269-318c6cf55123.png">





## Base structure

[AWS re:Invent 2020: Top 5 best practices for data streaming with Amazon Kinesis](https://www.youtube.com/watch?v=UE34CWAhT3o)

![image](https://user-images.githubusercontent.com/52392004/164177253-a4d812dc-61a3-49b5-8314-7bb58b134e4c.png)


## Cases


당근마켓: [DynamoDB 데이터 변경 이벤트 파이프라인 구축하기](https://medium.com/daangn/dynamodb-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B3%80%EA%B2%BD-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%ED%8C%8C%EC%9D%B4%ED%94%84%EB%9D%BC%EC%9D%B8-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0-feat-kinesis-1733db06066)

![image](https://user-images.githubusercontent.com/52392004/164145538-e6ecdad6-6f3e-45eb-94b0-9bc26dc21205.png)


[AWS Kinesis Data Stream 으로 대용량 데이터 수집을 편하게](https://medium.com/snaps-tech/aws-kinesis-data-stream-%EC%9C%BC%EB%A1%9C-%EB%8C%80%EC%9A%A9%EB%9F%89-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%88%98%EC%A7%91%EC%9D%84-%ED%8E%B8%ED%95%98%EA%B2%8C-f12610591496)

![image](https://user-images.githubusercontent.com/52392004/164145634-0f189d53-f384-4f6a-8b56-93e58b3160f6.png)

[AWS - Kinesis Data Stream - Hands On!](https://www.youtube.com/watch?v=ZErwfH-OLk4)
![image](https://user-images.githubusercontent.com/52392004/164145865-013d9270-f32f-4150-8825-086f575ee2e2.png)



## Reference 

[Amazon Kinesis Data Streams](https://aws.amazon.com/kinesis/data-streams/?nc1=h_ls)

[Amazon Kinesis Data Streams와 MSK를 비교해 보기](https://www.youtube.com/watch?v=9y-aCX5O3Ms)
