# Spark-Streaming

## 0.- Installation & Setup

<details><summary>Show 0.- Installation & Setup</summary>
<p>

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



</p>
</details>
