# Kinesis Data Stream 이란?

## How it works

Amazon Kinesis Data Streams is a **serverless streaming data service** that makes it easy to capture, process, and store data streams at any scale.

<img width="804" alt="image" src="https://user-images.githubusercontent.com/52392004/164144874-3337a267-03fa-469b-a53e-4410e9de6469.png">


## 사용 케이스 

1) Steam log and event data: Ingest and collect terabytes of data per day from application and service logs, clickstream data, sensor data, and in-app user events to power live dashboards, generate metrics, and deliver data into data lakes.

2) Run real-time analytics: Build applications for high-frequency event data such as clickstream data, and gain access to insights in seconds, not days, using AWS Lambda or Amazon Kinesis Data Analytics.

3) Power event-driven applications: Quickly pair with AWS Lambda to respond to or adjust immediate occurrences within the event-driven applications in your environment, at any scale.


## Base structure


![image](https://user-images.githubusercontent.com/52392004/164177253-a4d812dc-61a3-49b5-8314-7bb58b134e4c.png)

![image](https://user-images.githubusercontent.com/52392004/165636649-a866a0e5-c4ac-4026-bbb3-e6aec859e314.png)

## 특징 : Easily stream data at any scale

1) With Amazon Kinesis Data Streams, there are no servers to manage. The on-demand mode eliminates the need to provision or manage capacity required for running applications.

2) Adjust your capacity to stream gigabytes per second of data with Kinesis Data Streams. Get automatic provisioning and scaling with the on-demand mode.

3) Pay only for what you use with Kinesis Data Streams, starting as low as $0.015 per hour. With the on-demand mode, you don't need to worry about over-provisioning.

4) Use built-in integrations with other AWS services to create analytics, serverless, and application integration solutions on AWS quickly.


## Benefits of Stream storage

- Decouple producers & consumers

- Persistent buffer

- Collect multiple streams

- Preserve client ordering

- Parallel consumption






## Kafka 비교 

<img width="377" alt="image" src="https://user-images.githubusercontent.com/52392004/165637167-b2175d68-89de-44c7-809f-fa7534494dd8.png">

<img width="418" alt="image" src="https://user-images.githubusercontent.com/52392004/165637638-a287e1d5-b835-47d3-82e5-a92bb1125ac5.png">

PK: Partition Key 예) b8e0745459d9a885f1b30541e28e0e6c

[Kinesis Data Stream에 입력한 결과의 예

```java
kinesisResponse: { 
"ShardId": "shardId-000000000000", "SequenceNumber": "49628968760419381815775185092326431149216009853023027202" 
} 
```





## Cases


당근마켓: [DynamoDB 데이터 변경 이벤트 파이프라인 구축하기](https://medium.com/daangn/dynamodb-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B3%80%EA%B2%BD-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%ED%8C%8C%EC%9D%B4%ED%94%84%EB%9D%BC%EC%9D%B8-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0-feat-kinesis-1733db06066)

![image](https://user-images.githubusercontent.com/52392004/164145538-e6ecdad6-6f3e-45eb-94b0-9bc26dc21205.png)


[AWS Kinesis Data Stream 으로 대용량 데이터 수집을 편하게](https://medium.com/snaps-tech/aws-kinesis-data-stream-%EC%9C%BC%EB%A1%9C-%EB%8C%80%EC%9A%A9%EB%9F%89-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%88%98%EC%A7%91%EC%9D%84-%ED%8E%B8%ED%95%98%EA%B2%8C-f12610591496)

![image](https://user-images.githubusercontent.com/52392004/164145634-0f189d53-f384-4f6a-8b56-93e58b3160f6.png)

[AWS - Kinesis Data Stream - Hands On!](https://www.youtube.com/watch?v=ZErwfH-OLk4)
![image](https://user-images.githubusercontent.com/52392004/164145865-013d9270-f32f-4150-8825-086f575ee2e2.png)


## Capacity

### Write capacity (Maximum)

200 MiB/second, 200,000 records/second

### Read capacity (Maximum)

400 MiB/second



## Reference 

[AWS re:Invent 2020: Top 5 best practices for data streaming with Amazon Kinesis](https://www.youtube.com/watch?v=UE34CWAhT3o)


[Amazon Kinesis Data Streams](https://aws.amazon.com/kinesis/data-streams/?nc1=h_ls)

[Amazon Kinesis Data Streams와 MSK를 비교해 보기](https://www.youtube.com/watch?v=9y-aCX5O3Ms)
