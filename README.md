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
- Create New App - Name:"SparkStreamingExamples", Descriptioon:"Playing with Spark Streaming" > Yes, I agree > Create your Twitter application

</p>
</details>

</p>
</details>

## References

https://www.udemy.com/taming-big-data-with-spark-streaming-hands-on/
