To test the KafkaToS3 Streaming job do:

1. Start the Mesos cluster
2. Install Spark and Kafka ... and HDFS, since its tools provide basic S3 support
3. Add a topic
4. Create a fat jar containing all dependencies defined in Gradle with `./gradlew fatJar`
5. Upload the fat jar to a place accessible from the cluster e.g. S3
6. Create an [S3 bucket](https://console.aws.amazon.com/s3/home?region=us-west-1#) to store the backups and copy its URL 
6. Submit the spark job with:


`dcos spark run --submit-args="--supervise --conf spark.mesos.uris=http://hdfs.marathon.mesos:9000/v1/connect/hdfs-site.xml,http://hdfs.marathon.mesos:9000/v1/connect/core-site.xml --class com.zuehlke.hackzurich.KafkaToS3 jar-location topicName bucketName awsId awsSecret"`

