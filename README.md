# Scala-Spark-Streaming

## 1.- Installation & Setup

<details><summary>Show 0.- Installation & Setup</summary>
<p>
  
### Intalling JDK 8

<details><summary>Show Installing Spark</summary>
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
- Right Click "SparkStreamingExamples" > Properties > Scala Compiler > Check - Use Project Settings > Scala Installation: "Fixed Scala Installation: 2.11.8 (built-in)" > OK > OK

- Run > Run Configurations > Scala Application > Name:"PrintTweets", Main:"com.demo.sparkstreaming.PrintTweets" > Run

</p>
</details>

</p>
</details>

## References

https://www.udemy.com/taming-big-data-with-spark-streaming-hands-on/
