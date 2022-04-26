# SQS (Simple Queue Service)


### Visibility timeout

Visibility timeout은 메시지를 받는 시간 (length of time that a message received from a queue)를 의미합니다. 이 시간은 메시지를 가져간 application이 처리를 하고 queue에 있는 메시지를 삭제할때까지의 최대 시간을 의미 합니다. 

![image](https://user-images.githubusercontent.com/52392004/165202908-c5418eaf-a86f-4ef9-855a-5174b73367e5.png)

### Retention Period

The message retention period is the amount of time that Amazon SQS retains a message that does not get deleted. Amazon SQS automatically deletes messages that have been in a queue for more than the maximum message retention period. The default retention period is 4 days. The retention period has a range of 60 seconds to 1,209,600 seconds (14 days).

The expiration of a message is always based on its original enqueue timestamp. When a message is moved to a dead-letter queue, the enqueue timestamp remains unchanged. For example, if a message spends 1 day in the original queue before being moved to a dead-letter queue, and the retention period of the dead-letter queue is set to 4 days, the message is deleted from the dead-letter queue after 3 days. For this reason, we recommend that you always set the retention period of a dead-letter queue to be longer than the retention period of the original queue.


### Message Size

You can set the maximum message size for your queue. The smallest supported message size is 1 byte (1 character). The largest size is 262,144 bytes (256 KB). To send messages larger than 256 KB, you can use the Amazon SQS Extended Client Library for Java (https://github.com/awslabs/amazon-sqs-java-extended-client-lib). This library allows you to send an Amazon SQS message that contains a reference to a message payload in Amazon S3. The maximum payload size is 2 GB.


### How large can Amazon SQS message queues be?

A single Amazon SQS message queue can contain an unlimited number of messages. However, there is a quota of 120,000 for the number of inflight messages for a standard queue and 20,000 for a FIFO queue. Messages are inflight after they have been received from the queue by a consuming component, but have not yet been deleted from the queue.


## Reference 

[Amazon SQS 제한 시간 초과](https://docs.aws.amazon.com/ko_kr/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-visibility-timeout.html)

[Limits and restrictions](https://aws.amazon.com/sqs/faqs/?nc1=h_ls)
