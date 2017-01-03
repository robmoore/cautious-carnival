# Notes for setting up [Spark Notebook](http://spark-notebook.io/) example

1. Run the following commands:
    ```
    docker pull andypetrella/spark-notebook:0.7.0-scala-2.11.8-spark-2.0.2-hadoop-2.7.2
    docker pull cassandra
    docker run --name my-cassandra -d cassandra:latest # or docker start my-cassandra if already present
    docker run -p 9001:9001 --link my-cassandra andypetrella/spark-notebook:0.7.0-scala-2.11.8-spark-2.0.1-hadoop-2.7.2
    ```
1. Access [Spark Notebook](http://localhost:9001)
1. Drag and drop `Twitter to Cassandra.snb` on to the Spark Notebook files tab
1. Run `docker ps | grep my-cassandra | cut -f1 -d" "` to determine Cassandra instance hostname. 
Note: The IP address for the Cassandra instance is in the environment variables for the 
Spark Notebook instance.
1. Set up metadata (Edit -> Edit Metadata)
    ```
    "customLocalRepo": "/tmp/repo",
      "customDeps": [
        "com.datastax.spark % spark-cassandra-connector_2.11 % 2.0.0-M3",
        "org.apache.bahir % spark-streaming-twitter_2.11 % 2.0.1"
      ],
      "customSparkConf": {
        "spark.cassandra.connection.host": "<cassandra-hostname-here>"
      },
    ```
1. Execute cells in notebook

1. Set Twitter credentials using form in training example or do so in metadata?
1. Add Spark Twitter library dependencies in metadata
1. See `Twitter example` notebook that is bundled with distribution


## Reference
- [Github repo](https://github.com/andypetrella/spark-notebook/) for Spark Notebook 
- From O'Reilly class: `docker run --rm -it -m 8g --net=host datafellas/distributed-pipeline-quotes:2.0.1 bash`
- Using [Spark Twitter libraries](http://bahir.apache.org/docs/spark/current/spark-streaming-twitter/)
- Example [project](https://medium.com/@anicolaspp/spark-streaming-and-twitter-sentiment-analysis-c860938d484#.my55l8ggh) 
of sentiment analysis on Tweets using Spark
- https://github.com/andypetrella/spark-notebook/blob/master/docs/metadata.md#custom-variables
- Also, see configuration example from `training-exercices-Assessment 1.snb`
- Useful info in both `training-exercices-Assessment 1.snb` and `training-exercices-Assessment 2.snb`
- http://ampcamp.berkeley.edu/3/exercises/realtime-processing-with-spark-streaming.html
- https://dev.twitter.com/streaming/public
- https://github.com/apache/bahir/blob/master/streaming-twitter/examples/src/main/scala/org/apache/spark/examples/streaming/twitter/TwitterPopularTags.scala
- https://github.com/apache/bahir/tree/master/streaming-twitter
- http://bahir.apache.org/docs/spark/2.0.1/spark-streaming-twitter/
- https://gitter.im/andypetrella/spark-notebook

## Things to try
1. Run the `TwitterPopularTags.scala` example from above to test the feed works with the Spark API.
1. Try using local version of Spark instead of Docker version
1. Try using Twitter4j directly (see https://github.com/yusuke/twitter4j/blob/master/twitter4j-examples/src/main/java/twitter4j/examples/stream/PrintSampleStream.java)

## From last night
- Use `streaming-Twitter stream.snb` to get a Twitter stream up and running

## For testing
`twurl -t -H stream.twitter.com /1.1/statuses/sample.json`

## Env variables dump

```
import scala.collection.JavaConversions._

val environmentVars = System.getenv()
for ((k,v) <- environmentVars) println(s"key: $k, value: $v")

val properties = System.getProperties()
for ((k,v) <- properties) println(s"key: $k, value: $v")
```