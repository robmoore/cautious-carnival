# Notes for setting up [Spark Notebook](http://spark-notebook.io/) example

```
docker pull andypetrella/spark-notebook:0.7.0-scala-2.11.8-spark-2.0.2-hadoop-2.7.2
docker pull cassandra
docker run --name my-cassandra -d cassandra:latest
docker run -p 9001:9001 --link my-cassandra andypetrella/spark-notebook:0.7.0-scala-2.11.8-spark-2.0.1-hadoop-2.7.2
```

1. Docker inspect to determine Cassandra instance IP
1. Set up metadata (Note that setting it in notebook cell wasn't successful)
```
"customLocalRepo": "/tmp/repo",
  "customDeps": [
    "com.datastax.spark % spark-cassandra-connector_2.11 % 2.0.0-M3"
  ],
  "customSparkConf": {
    "spark.cassandra.connection.host": "172..."
  },
```
## Reference
- [Github](https://github.com/andypetrella/spark-notebook/) site for Spark Notebook 
- From class: `docker run --rm -it -m 8g --net=host datafellas/distributed-pipeline-quotes:2.0.1 bash`
- Using [Spark Twitter libraries](http://bahir.apache.org/docs/spark/current/spark-streaming-twitter/)
- Example [project](https://medium.com/@anicolaspp/spark-streaming-and-twitter-sentiment-analysis-c860938d484#.my55l8ggh) of sentiment analysis with Spark on Tweets
- https://github.com/andypetrella/spark-notebook/blob/master/docs/metadata.md#custom-variables
- Also, see configuration example from `training-exercices-Assessment 1.snb`

## Keep in mind
- When the Cassandra example worked it was with cassandra:2.1 docker instance
- Used IP instead of hostname for Cassandra instance

