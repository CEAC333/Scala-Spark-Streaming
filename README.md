# Scala-Spark-Streaming

## 1.- Installation & Setup

<details><summary>Show 1.- Installation & Setup</summary>
<p>
  
### Intalling JDK 8

<details><summary>Show Installing JDK 8</summary>
<p>
  
- Download and Install - http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
  
</p>
</details>

### Installing Spark

<details><summary>Show Installing Spark</summary>
<p>

#### MacOS

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install apache-spark
```

Change the version "2.2.1" for the actual version installed
```shell
cd /usr/local/Cellar/apache-spark/2.2.1/libexec/conf cp log4j.properties.template log4j.properties
```

Edit the log4j.properties file and change the log level from INFO to ERROR on log4j.rootCategory
```shell
nano log4j.properties.template
```

</p>
</details>

### Installing Scala IDE

<details><summary>Show Installing Scala IDE</summary>
<p>

#### MacOS
- Download and Install - http://scala-ide.org/download/sdk.html


</p>
</details>

### First Spark Streaming App 

<details><summary>Show First Spark Streaming App</summary>
<p>
  
- Create a Twitter Developer Account and Sign in - https://apps.twitter.com/
- Create New App - Name:"SparkStreamingExamples", Description:"Playing with Spark Streaming" > Yes, I agree > Create your Twitter application
- Keys and Access Tokens > Create my access token
- Copy the consumerKey, consumerSecret, accessToken and accessTokenSecret inside the twitter.txt file

```shell
consumerKey XXX-someawesome-key
consumerSecret XXX-someawesome-key
accessToken XXX-someawesome-key
accessTokenSecret XXX-someawesome-key
```

- Scala IDE > File > New Scala Project > Name:"SparkStreamingExamples" > Finish
- Right Click "SparkStreamingExamples" > New > Package > Name:"com.demo.sparkstreaming"
- Right Click "SparkStreamingExamples" > Properties > Java Build Path > Libraries > Add External JARS... > Select all in spark/jars > Add External JARS... > Select "twitter4j-core...jar", "twitter4j-stream...jar", "dstream-twitter...jar"
- Right Click "com.demo.sparkstreaming" > Import > General > File System > Next > From directory:"Choose dir with PrintTweets.scala  & Utilities.scala files" > Finish
- Right Click "SparkStreamingExamples" > Properties > Scala Compiler > Check - Use Project Settings > Scala Installation: "Fixed Scala Installation: 2.11.X (built-in)" > OK > OK

- Run > Run Configurations > Scala Application > Name:"PrintTweets", Main:"com.demo.sparkstreaming.PrintTweets" > Run

Utilities.scala
```scala
package com.demo.sparkstreaming

import org.apache.log4j.Level
import java.util.regex.Pattern
import java.util.regex.Matcher

object Utilities {
    /** Makes sure only ERROR messages get logged to avoid log spam. */
  def setupLogging() = {
    import org.apache.log4j.{Level, Logger}   
    val rootLogger = Logger.getRootLogger()
    rootLogger.setLevel(Level.ERROR)   
  }
  
  /** Configures Twitter service credentials using twiter.txt in the main workspace directory */
  def setupTwitter() = {
    import scala.io.Source
    
    for (line <- Source.fromFile("../twitter.txt").getLines) {
      val fields = line.split(" ")
      if (fields.length == 2) {
        System.setProperty("twitter4j.oauth." + fields(0), fields(1))
      }
    }
  }
  
  /** Retrieves a regex Pattern for parsing Apache access logs. */
  def apacheLogPattern():Pattern = {
    val ddd = "\\d{1,3}"                      
    val ip = s"($ddd\\.$ddd\\.$ddd\\.$ddd)?"  
    val client = "(\\S+)"                     
    val user = "(\\S+)"
    val dateTime = "(\\[.+?\\])"              
    val request = "\"(.*?)\""                 
    val status = "(\\d{3})"
    val bytes = "(\\S+)"                     
    val referer = "\"(.*?)\""
    val agent = "\"(.*?)\""
    val regex = s"$ip $client $user $dateTime $request $status $bytes $referer $agent"
    Pattern.compile(regex)    
  }
}
```

PrintTweets.scala
```scala


package com.demo.sparkstreaming

import org.apache.spark._
import org.apache.spark.SparkContext._
import org.apache.spark.streaming._
import org.apache.spark.streaming.twitter._
import org.apache.spark.streaming.StreamingContext._
import org.apache.log4j.Level
import Utilities._

/** Simple application to listen to a stream of Tweets and print them out */
object PrintTweets {
 
  /** Our main function where the action happens */
  def main(args: Array[String]) {

    // Configure Twitter credentials using twitter.txt
    setupTwitter()
    
    // Set up a Spark streaming context named "PrintTweets" that runs locally using
    // all CPU cores and one-second batches of data
    val ssc = new StreamingContext("local[*]", "PrintTweets", Seconds(1))
    
    // Get rid of log spam (should be called after the context is set up)
    setupLogging()

    // Create a DStream from Twitter using our streaming context
    val tweets = TwitterUtils.createStream(ssc, None)
    
    // Now extract the text of each status update into RDD's using map()
    val statuses = tweets.map(status => status.getText())
    
    // Print out the first ten
    statuses.print()
    
    // Kick it all off
    ssc.start()
    ssc.awaitTermination()
  }  
}
```

</p>
</details>

</p>
</details>

## References

https://www.udemy.com/taming-big-data-with-spark-streaming-hands-on/
