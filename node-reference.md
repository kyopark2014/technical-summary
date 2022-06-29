# Node Reference

## Dynamodb에 쓰기

```java
const tableName = process.env.tableName;

let putParams = {
  TableName: tableName,
  Item: {
    "user-id": input["user-id"],
    "name": input["name"],
  } 
};

try {
  await dynamo.put(putParams).promise();
} catch (error) {
  console.log('Failure: '+error);
}
```

## DynamoDB 전체 읽기 

```java
const queryParams = {
  TableName: tableName
};
        
var dynamoQuery; 
try {
  dynamoQuery = await dynamo.scan(queryParams).promise();

  results = dynamoQuery.Items;
    
  console.log('queryDynamo: '+dynamoQuery.Count);   
} catch (error) {
  console.log('Failure: '+error);
  return;
} 
```        
