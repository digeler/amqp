Amqp on  azure 
this demonstrates using amqp with azure eventhub.

clone the repo 


change the parameters in the sh files to match your eventhub
build the image.

to create the reciever :
run the following : 

docker run -itd dockerimage sh recieve.sh 
check the logs you should see the following :

[Event Hub] 2018/09/20 04:37:36 Done flushing to file the current partition offsets '[3832 3920]' at path ./assets/main_receiver_offsets.csv
[Event Hub] 2018/09/20 04:37:36 Done flushing to file the current partition offsets '[3832 3920]' at path ./assets/main_receiver_offsets.csv
[Event Hub] 2018/09/20 04:37:37 Done flushing to file the current partition offsets '[3832 3920]' at path ./assets/main_receiver_offsets.csv
[Event Hub] 2018/09/20 04:37:38 Done flushing to file the current partition offsets '[3832 3920]' at path ./assets/main_receiver_offsets.csv
[Event Hub] 2018/09/20 04:37:39 Done flushing to file the current partition offsets '[3832 3920]' at path ./assets/main_receiver_offsets.csv
[Event Hub] 2018/09/20 04:37:40 Done flushing to file the current partition offsets '[3832 3920]' at path ./assets/main_receiver_offsets.csv
[Event Hub] 2018/09/20 04:37:40 Done flushing to file the current partition offsets '[3832 3920]' at path ./assets/main_receiver_offsets.csv
[Event Hub] 2018/09/20 04:37:41 Done flushing to file the current partition offsets '[3832 3920]' at path ./assets/main_receiver_offsets.csv
[Event Hub] 2018/09/20 04:37:42 Done flushing to file the current partition offsets '[3832 3920]' at path ./assets/main_receiver_offsets.csv


to create the sender :

docker run -itd dockerimage sh sender.sh

* when you run this check  the reciever container

check the logs :
[Event Hub] 2018/09/19 17:47:39 The TLS configuration is storing the SSL key at './sslkey.log'
[Event Hub] 2018/09/19 17:47:39 The AMQP connection is ready for the namespace 'jbhubevent'
[Event Hub] 2018/09/19 17:47:39 Using this Event Hub URI: 'amqp://jbhubevent.servicebus.windows.net/tester'
[Event Hub] 2018/09/19 17:47:39 The expiry interval for the SASL token is: 1537379279
[Event Hub] 2018/09/19 17:47:39 The new Microsoft SASL token is: SharedAccessSignature sig=3DVnVfmbsKZN7Rd0aredAccessKey&sr=amqp%3a%2f%2fjbhubevent.servicebus.windows.net%2ftester
[Event Hub] 2018/09/19 17:47:39 Established AMQP link to send messages to the Event Hub: 'tester' 

once sending the message on the reciever you should see :

Event Hub] 2018/09/20 04:42:50 This AMQP link: 'amqp_receiver_8@2(<-tester/ConsumerGroups/$Default/Partitions/0)', received a message, the transformed to send is: {"body":"Sending just ONE at timestamp 2018-09-20 04:42:44.926347715 +0000 UTC","sequence_number":22,"partiton_key":"","offset":"4016","enqueued_time":"2018-09-20T04:33:20Z","eh_endpoint":"amqp_receiver_8@2(\u003c-tester/ConsumerGroups/$Default/Partitions/0)","partition_id":0,"application_properties":{}}
[Event Hub] 2018/09/20 04:42:50 The received msg (to update the in-memory offsets): {"body":"Sending just ONE at timestamp 2018-09-20 04:42:44.926347715 +0000 UTC","sequence_number":22,"partiton_key":"","offset":"4016","enqueued_time":"2018-09-20T04:33:20Z","eh_endpoint":"amqp_receiver_8@2(\u003c-tester/ConsumerGroups/$Default/Partitions/0)","partition_id":0,"application_properties":{}}
[Event Hub] 2018/09/20 04:42:50 Done updating the current partition offsets '[4016 3920]' with the new value '4016' with partitionID '0'


