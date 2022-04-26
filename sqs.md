# SQS (Simple Queue Service)


### Retention Period: up to 14 days

The message retention period is the amount of time that Amazon SQS retains a message that does not get deleted. Amazon SQS automatically deletes messages that have been in a queue for more than the maximum message retention period. The default retention period is 4 days. The retention period has a range of 60 seconds to **1,209,600 seconds (14 days)**.


### Message Size: less than 256KB

You can set the maximum message size for your queue. The smallest supported message size is 1 byte (1 character). The largest size is 262,144 bytes (256 KB). To send messages larger than **256 KB**, you can use the Amazon SQS Extended Client Library for Java (https://github.com/awslabs/amazon-sqs-java-extended-client-lib). This library allows you to send an Amazon SQS message that contains a reference to a message payload in Amazon S3. The maximum payload size is 2 GB.


### How large can Amazon SQS message queues be? 120,000(standard), 20,000(FIFO)

A single Amazon SQS message queue can contain an unlimited number of messages. However, there is a quota of **120,000** for the number of inflight messages for a standard queue and **20,000** for a FIFO queue. Messages are inflight after they have been received from the queue by a consuming component, but have not yet been deleted from the queue.

### Visibility timeout

Visibility timeout은 메시지를 받는 시간 (length of time that a message received from a queue)를 의미합니다. 이 시간은 메시지를 가져간 application이 처리를 하고 queue에 있는 메시지를 삭제할때까지의 최대 시간을 의미 합니다. 

![image](https://user-images.githubusercontent.com/52392004/165202908-c5418eaf-a86f-4ef9-855a-5174b73367e5.png)


### Dead-letter queues

If a message can't be consumed successfully, you can send it to a dead-letter queue (DLQ). Dead-letter queues let you isolate problematic messages to determine why they are failing.

When you designate a queue to be a source queue, a DLQ is not created automatically. You must first create a queue to designate as the DLQ. The DLQ queue type (standard or FIFO) must match the source queues. You can associate the same DLQ with more than one source queue.

The Maximum receives value determines when a message will be sent to the DLQ. If the ReceiveCount for a message exceeds the maximum receive count for the queue, Amazon SQS moves the message to the associated DLQ (with its original message ID).

You must use the same AWS account to create the DLQ and the source queues that send messages to the DLQ. Also, the DLQ must reside in the same region as the source queues that use the DLQ.


![image](https://user-images.githubusercontent.com/52392004/165347919-97834736-b8d2-4885-a996-41b90580debf.png)



## Reference 

[Amazon SQS 제한 시간 초과](https://docs.aws.amazon.com/ko_kr/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-visibility-timeout.html)

[Limits and restrictions](https://aws.amazon.com/sqs/faqs/?nc1=h_ls)
