# Call Center Analytics

AI/ML 기술의 발전으로 Call Center의 지능화가 진행되고 있습니다. Amazon Connect는 Call Center에 필요한 각종 솔루션을 제공하고 있습니다. 아래에서는 Amazon Connect에서 수집된 상담내역(Customer Trace Record) 등의 데이터를 어떻게 분석할 것인지에 대한 솔루션을 검토하고자 합니다. 

기본적인 Call Center Architecture는 아래와 같습니다.

<img width="817" alt="image" src="https://user-images.githubusercontent.com/52392004/167278378-eb719a86-1fe5-45a1-bcad-28efde9ddd99.png">

여기서, Contact Trace Records(CTR)관련된 Analytics만 표시하면 아래와 같습니다.

![image](https://user-images.githubusercontent.com/52392004/167281286-17943959-9ec2-473e-a868-28586d43782e.png)

1) 고객(Customer)가 Call Center로 전화를 하고, 상담원(Agent)와 연결되면, 통화이력, 상담내용 등에 대한 Customer Trace Record (CTR)이 생성됩니다. 

2) 생성된 CTR들은 Amazon Kinesis Data Stream을 통해 수집되고, Kinesis Data Firehose와 Glue Data Catalog를 통해 Parquet와 같은 파일로 변환 후 S3에 저장됩니다.

3) 필요시 AWS Lambda를 통해 record를 변환하여 사용합니다.

4) Amazon S3에 저장된 CTR들은 Amazon Athena로 분석될 수 있으며, Amazon QuickSight로 상세한 현황을 확인할 수 있습니다. 



## Reference 

1) Advanced Serverless Architectural Patterns on AWS (2019)


![image](https://user-images.githubusercontent.com/52392004/163650956-5c269578-5202-4db8-9df2-b5a0fe52f4fa.png)

[Advanced Serverless Architectural Patterns on AWS](https://www.youtube.com/watch?v=o9YB2F3pCHU)

Alex Casalboni, Sr. Technical Evangelist in AWS

2) Data Conversion

![image](https://user-images.githubusercontent.com/52392004/163651834-8294f6a1-e8e4-4551-8ae0-c6cb01b25a7b.png)

- Save space and enable faster queries compared to row-oriented formats like JSON.

- Convert the format of your input data from JSON to columnar data format Apache Parquet or Apache ORC before storing the data in Amazon S3.

- Works in conjunction to the transform features to convert other format to JSON before the data conversion




