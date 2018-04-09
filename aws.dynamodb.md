- [DynamoDB in a Spring Boot Application Using Spring Data](http://www.baeldung.com/spring-data-dynamodb)
- [start DynamoDB instance locally automatically from Spring context](https://stackoverflow.com/questions/26901613/easier-dynamodb-local-testing/37780083#37780083)
- https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/AppendixSampleDataCodeJava.html

## Step function
- no state > 32kb
- no way to update function in place

## dynamodb Streams
- Local Secondary Index (LSI)
  * JobId & Score
- Global secondary index (GSI)
  * UserId & TimeApplied
  * maximum 5 GSIs per table
  * GSI can be created anytime
  * partition key and Sort key do not need to be unique
- LSI(Local Secondary Index) v.s. GSI(Global secondary index)
  * max 5 per table
  * only created on table creation v.s. GSI can be created anytime
  * LSI share wcu and rcu v.s. GSI have dedicated WCU and RCU
  * consistent and eventually consistent modes v.s. GSI eventually consistent reads only

## [composite primary key](https://stackoverflow.com/questions/32620215/3-fields-composite-primary-key-unique-item-in-dynamodb)
- cannot have more than two attributes form your primary key (hash+range)
