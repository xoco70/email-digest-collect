# email-digest
Hourly email digest

#### Assumptions
* Message has to processed based on timestamp/per user so that we can send email digest by timestamp
* 

### Current solution implemented using Spring cloud AWS, SNS HTTP subscription and MongoDB
* Send message from SNS to Ra for message backup as system may go down.
* Poll maximum number of messages from SQS after every 1 hour 
* Send an email
##### Current execution flow
* Consume the message through HTTP(Spring Cloud AWS messaging) in backend
* Write the message to MongoDB
* Schedular poll all messages in timestamp range
* Send email 

### Solution using SNS vs SQS Subscription 
##### Pros
* Messages can be backup for few days out of the box so that never worry about downtime.
* 
##### Cons
* Amazon SNS isn't currently compatible with SQS FIFO queues. For us order matters as per my understanding.
* Not sure number of message can be processed by SQS, what if SNS produces huge messages and to consider we process once in an hour!

### Solution using Spring cloud AWS, SNS HTTP subscription and File System 
##### Pros
* Messages can be streamed to file in specific format and we can streams back to process after every 1 hour
* 
##### Cons
* Hard to query
* Distributed locking?
* 

### Solution using Spring cloud AWS, SNS HTTP subscription and RabbitMQ 
##### Pros
* No Db, so performance can be gain
* 
##### Cons
* Messaging order issue, need to put efforts!!


### References
* http://engineering.pamediakopes.gr/2015/10/12/sns-a-love-and-hate-story/  
* https://www.quora.com/What-is-the-difference-between-Kinesis-and-SQS-It-seems-capable-of-serving-similar-use-cases-apart-from-the-shards-and-partition-keys
 