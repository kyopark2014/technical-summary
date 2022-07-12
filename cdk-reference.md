# CDK Reference Codes

CDK의 reference code들을 여기에 모아서 편히 보도록 합니다. 

## 유용한 Samples

#### [TwinMaker를 위한 IoT Data Generator 생성하기](https://github.com/kyopark2014/iot-data-generator-for-twinmaker/blob/main/cdk-twinmaker/lib/cdk-twinmaker-stack.ts)

IoT Core, IoT Rule, IoT SiteWise (AssetModel, Asset), IoT TwinMaker, S3

Multi Stack

#### [IoT Data Generator를 이용하여 다양한 Data Source를 생성하고 Timestream과 Grafana를 이용하여 Dashboard 생성하기](https://github.com/kyopark2014/iot-data-generator/blob/main/cdk-timestream/lib/cdk-timestream-stack.ts)

IoT Core, IoT Rule, Timestream

#### [AWS IoT Edukit 이용한 Analytic Environment](https://github.com/kyopark2014/iot-analytics-for-thermometer/blob/main/cdk-iot/lib/cdk-iot-stack.ts)

IoT Core, IoT Rule, Kinesis Data Streams, Kinesis Data Firehose, S3, Lambda, Athena, API Gateway, CloudFront, SNS

#### [Lambda Function URL](https://github.com/kyopark2014/lambda-function-url/blob/main/cdk-lambda/lib/cdk-lambda-stack.ts)

Lambda Function URL, DynamoDB

#### [Case Study: "Wait for Callback" 구현](https://github.com/kyopark2014/case-study-wait-for-callback/blob/main/cdk-callback/lib/cdk-callback-stack.ts)

EventBridge, Step Functions, Lambda, SNS, API Gateway

#### [AWS CloudFront의 URL Routing을 이용한 Web Client 및 API Server 구현](https://github.com/kyopark2014/aws-routable-cloudfront/blob/main/cdk-cloudfront/lib/cdk-cloudfront-stack.ts)

CloudFront, API Gateway, Lambda, S3

#### [API Gateway로 Query string을 포함한 RESTful API 구현하기](https://github.com/kyopark2014/apigw-rest-querystring/blob/main/cdk-restapi/lib/cdk-restapi-stack.ts)

Lambda, API Gateway

#### [PinPoint를 이용한 Campaign 생성](https://github.com/kyopark2014/campaign-producer-for-pinpoint/blob/main/lib/campaign-producer-for-pinpoint-stack.ts)

S3, CloudFront, PinPoint, API Gateway, Labmda

#### [CDK 기반의 Storytime](https://github.com/kyopark2014/cdk-storytime/blob/main/cdk-story/lib/cdk-story-stack.ts)

CloudFront, API Gateway, S3, SQS, SNS, Lambda, DynamoDB


## S3로 파일 복사

[aws-routable-cloudfront](https://github.com/kyopark2014/aws-routable-cloudfront/blob/main/cdk-cloudfront/lib/cdk-cloudfront-stack.ts) 을 참조합니다.

```java
import * as s3Deploy from "aws-cdk-lib/aws-s3-deployment"

    const s3Bucket = new s3.Bucket(this, "s3-bucket-for-web-application",{
      bucketName: "storage-web-application",
      blockPublicAccess: s3.BlockPublicAccess.BLOCK_ALL,
      removalPolicy: cdk.RemovalPolicy.DESTROY,
      autoDeleteObjects: true,
      publicReadAccess: false,
      versioned: false,
    });
    
    // copy web application files into s3 bucket
    new s3Deploy.BucketDeployment(this, "DeployWebApplication", {
      sources: [s3Deploy.Source.asset("../webapplication")],
      destinationBucket: s3Bucket,
    });
```



## Amazon S3

S3 Bucket 생성하고, bucket name, bucket arn, s3 path를 확인합니다. 

```java
    const s3Bucket = new s3.Bucket(this, "cdk-businfo",{
      removalPolicy: cdk.RemovalPolicy.DESTROY,
      autoDeleteObjects: true,
      publicReadAccess: false,
      versioned: false,
    });
    new cdk.CfnOutput(this, 'bucketName', {
      value: s3Bucket.bucketName,
      description: 'The nmae of bucket',
    });
    new cdk.CfnOutput(this, 's3Arn', {
      value: s3Bucket.bucketArn,
      description: 'The arn of s3',
    });
    new cdk.CfnOutput(this, 's3Path', {
      value: 's3://'+s3Bucket.bucketName,
      description: 'The path of s3',
    });
```    

## CloudFront
```java
    const distribution = new cloudFront.Distribution(this, 'storytime', {
      defaultBehavior: {
        origin: new origins.S3Origin(s3Bucket),
        allowedMethods: cloudFront.AllowedMethods.ALLOW_ALL,
        priceClass: cloudFront.PriceClass.PriceClass200,  
        viewerProtocolPolicy: cloudFront.ViewerProtocolPolicy.REDIRECT_TO_HTTPS,
        discription: 'cdk cloudFront'
      },
    });

    new cdk.CfnOutput(this, 'distributionDomainName', {
      value: distribution.domainName,
      description: 'The domain name of the Distribution',
    }); 
```


## kinesis data stream

Kinesis Data Stream을 정의하고 stream ARN을 확인하는 방법입니다. matric도 추가 할 수 있습니다. 

```java
    const stream = new kinesisstream.Stream(this, 'Stream', {
      streamName: 'businfo',
      retentionPeriod: cdk.Duration.hours(48),
      streamMode: kinesisstream.StreamMode.ON_DEMAND
    });

    new cdk.CfnOutput(this, 'StreamARN', {
      value: stream.streamArn,
      description: 'The arn of kinesis stream',
    });

    // using pre-defined metric method
    stream.metricGetRecordsSuccess();
    stream.metricPutRecordSuccess();
```    

## SQS
```java
    const queueRekognition = new sqs.Queue(this, 'QueueRekognition');

    new cdk.CfnOutput(this, 'sqsRekognitionUrl', {
      value: queueRekognition.queueUrl,
      description: 'The url of the Rekognition Queue',
    });
```

## SNS
```java
    const topic = new sns.Topic(this, 'sns-storytime', {
      topicName: 'sns-storytime'
    });
    topic.addSubscription(new subscriptions.EmailSubscription('storytimebot21@gmail.com'));

    new cdk.CfnOutput(this, 'snsTopicArn', {
      value: topic.topicArn,
      description: 'The arn of the SNS topic',
    });
```

## DynamoDB
```java
    const dataTable = new dynamodb.Table(this, 'dynamodb-storytime', {
      tableName: 'dynamodb-storytime',
        partitionKey: { name: 'Id', type: dynamodb.AttributeType.STRING },
        sortKey: { name: 'Timestamp', type: dynamodb.AttributeType.STRING },
        billingMode: dynamodb.BillingMode.PAY_PER_REQUEST,
        // readCapacity: 1,
        // writeCapacity: 1,
        removalPolicy: cdk.RemovalPolicy.DESTROY,
    });
    dataTable.addGlobalSecondaryIndex({ // GSI
      indexName: 'ContentID-index',
      partitionKey: { name: 'ContentID', type: dynamodb.AttributeType.STRING },
    });
```    


## Lambda
```java
    const lambdaUpload = new lambda.Function(this, "LambdaUpload", {
      runtime: lambda.Runtime.NODEJS_14_X, 
      code: lambda.Code.fromAsset("repositories/serverless-storytime-for-upload"), 
      handler: "index.handler", 
      timeout: cdk.Duration.seconds(10),
      environment: {
        sqsRekognitionUrl: queueRekognition.queueUrl,
        sqsOpensearchUrl: queueOpensearch.queueUrl,
        topicArn: topic.topicArn,
        bucket: s3Bucket.bucketName
      }
    });  
    queueRekognition.grantSendMessages(lambdaUpload);
    queueOpensearch.grantSendMessages(lambdaUpload);
    dataTable.grantReadWriteData(lambdaUpload);
    topic.grantPublish(lambdaUpload);
    s3Bucket.grantReadWrite(lambdaUpload);
```

## Lambda (Cron Job)

```java
    const lambdaBusInfo = new lambda.Function(this, "LambdaBusInfo", {
      runtime: lambda.Runtime.NODEJS_14_X, 
      code: lambda.Code.fromAsset("repositories/get-businfo"), 
      handler: "index.handler", 
      timeout: cdk.Duration.seconds(10),
      environment: {
        tableName: tableName,
      }
    });  
    dataTable.grantReadWriteData(lambdaBusInfo);

    const rule = new events.Rule(this, 'Cron', {
      description: "Schedule a Lambda to save arrival time of buses",
      schedule: events.Schedule.expression('rate(1 minute)'),
    }); 
    rule.addTarget(new targets.LambdaFunction(lambdaBusInfo));
```

## Policy for Rekognition

create a policy statement

```java
    const RekognitionPolicy = new iam.PolicyStatement({
      actions: ['rekognition:*'],
      resources: ['*'],
    });
```    

add the policy to the Function's role

```java
    lambdaRekognition.role?.attachInlinePolicy(
      new iam.Policy(this, 'rekognition-policy', {
        statements: [RekognitionPolicy],
      }),
    );
```

## Policy for Polly

```java
    // create a policy statement
    const PollyPolicy = new iam.PolicyStatement({
      actions: ['polly:*'],
      resources: ['*'],
    });
    // add the policy to the Function's role
    lambdaPolly.role?.attachInlinePolicy(
      new iam.Policy(this, 'polly-policy', {
        statements: [PollyPolicy],
      }),
    );
```

## [Role](https://github.com/aws-samples/aws-iot-twinmaker-samples/blob/main/src/modules/sitewise/cdk/lib/sitewise-stack.js)

```java
        // The code that defines your stack goes here
        const iottwinmaker_connector_role = new iam.Role(this, 'iottwinmaker_connector_role', {
            assumedBy: new iam.CompositePrincipal(
                new iam.ServicePrincipal('lambda.amazonaws.com'),
                new iam.ServicePrincipal('states.amazonaws.com'),
                new iam.ServicePrincipal('events.amazonaws.com'),
                new iam.ServicePrincipal('iottwinmaker.amazonaws.com')
            ),
            managedPolicies: [
                iam.ManagedPolicy.fromAwsManagedPolicyName('AmazonS3FullAccess'),
                iam.ManagedPolicy.fromAwsManagedPolicyName('CloudWatchLogsFullAccess'),
                iam.ManagedPolicy.fromAwsManagedPolicyName('AWSStepFunctionsReadOnlyAccess'),
                iam.ManagedPolicy.fromAwsManagedPolicyName('SecretsManagerReadWrite')
            ]
        });
        const policy = new iam.ManagedPolicy(this, "IoTTwinMakerFullAccessPolicy", {
            statements: [
                new iam.PolicyStatement({
                    effect: iam.Effect.ALLOW,
                    actions: ["*"],
                    resources: ["*"]
                })
            ],
            roles: [iottwinmaker_connector_role]
        });
```

## Multiple principals 

1) 방안1

```java
    const Role = new iam.Role(this, 'LambdaRole', {
      // assumedBy: new iam.ServicePrincipal('lambda.amazonaws.com'),
      description: 'Role for lambda function url',
      assumedBy: new iam.CompositePrincipal(
        new iam.ServicePrincipal("lambda.amazonaws.com"),
        new iam.AccountPrincipal(cdk.Stack.of(this).account),
      ),
    });
```

2) 방안2 

```java
    const Role = new iam.Role(this, 'LambdaRole', {
      assumedBy: new iam.ServicePrincipal('lambda.amazonaws.com'),
      description: 'Role for lambda function url',
    });
    
    Role.assumeRolePolicy?.addStatements(
      new iam.PolicyStatement({
        actions: ['sts:AssumeRole'],
        effect: iam.Effect.ALLOW,
        principals: [new iam.AccountPrincipal(cdk.Stack.of(this).account)]
      })
    ); 
```    
    
