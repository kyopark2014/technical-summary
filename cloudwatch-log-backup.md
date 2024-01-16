# CloudWatch의 로그 Backup

[Exporting log data to Amazon S3](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/S3ExportTasksConsole.html)와 같이 Console 또는 CLI로 설정이 가능합니다.

1) cloudwatch에서 로그 폴더를 지정하고, Action에서 “Export data to Amazon S3”를 선택합니다.

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/b7920b10-ce30-48a2-8bc7-818a57ad92ca)

2) 날짜 지정하고 bucket을 지정한후 export 합니다.

![image](https://github.com/kyopark2014/technical-summary/assets/52392004/10471a26-75d4-4a70-97f2-2651003324e0)

bucket은 아래와 같은 퍼미션이 설정되어 있어야 합니다.

```java
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "logs.ap-northeast-2.amazonaws.com"
            },
            "Action": "s3:PutObject",
            "Resource": [
                "arn:aws:s3:::cdk-businfo",
                "arn:aws:s3:::cdk-businfo/*"
            ],
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "123456789012",
                    "s3:x-amz-acl": "bucket-owner-full-control"
                },
                "ArnLike": {
                    "aws:SourceArn": "arn:aws:logs:ap-northeast-2:123456789012:log-group:*"
                }
            }
        }
    ]
}
```
