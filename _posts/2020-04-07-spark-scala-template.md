---
layout: post
title: Application Template for Spark Scala with Gradle
subtitle: Sharing my tips for developing an application in local desktop and automating the complete build process using Apache Spark with Scala
image: /img/blog-1-spark-template.png
---

Apache Spark is the unified analytics engine for large scale data processing. Although it supports writing applications in Java/Scala/Python/R/SQL, Scala is preferred by many(especially by me) to develop applications due to its engine's nativity. Further, developing applications utilizing Spark in local desktop, automating build, testing and distribution can be done in multiple ways - Gradle based build automation is one of the option.

This tutorial will guide you to get started with a full fledged Spark application in local desktop with complete unit testing and build automation.

## Prerequisites
* JDK 1.8 - use jenv to manage Java Environments if required.

* Intellij or Eclipse for Integrated Development Environment(IDE).

* Scala plugin in case of IDE.

## Build with Gradle
Gradle; an open source build automation tool expressed in Groovy is used for accelerating the developer productivity. Gradle wrapper is used for  installing and maintaining the version stability across any environment. 

Setup the Gradle wrapper using this.

Below topics will help to define the project properties through build script "build.gradle" for the application using Spark.

## Managing Dependencies
* Spark libraries are expressed as "compileOnly" dependencies as they are available in the Spark clusters where the job will be executed.

* Other dependent libraries are expressed as "compile" which are further packaged in final application distribution.

* Test dependencies are expressed as "testCompile".

* Test dependencies can extend "compileOnly" for utilizing the spark libraries.

```
dependencies {
  compileOnly group: "org.apache.spark", name: "spark-core_2.11", version: "2.4.5"
  compileOnly group: "org.apache.spark", name: "spark-sql_2.11", version: "2.4.5"
  compileOnly group: "org.apache.spark", name: "spark-hive_2.11", version: "2.4.5"
  compile group: "org.scala-lang", name: "scala-library", version: "2.11.+"
  compile group: "ch.qos.logback", name: "logback-classic", version: "1.2.3"
  compile group: "org.slf4j", name: "log4j-over-slf4j", version: "1.7.25"
  compile group: "com.github.scopt", name: "scopt_2.11", version: "3.7.1"
  testCompile group: "com.holdenkarau", name: "spark-testing-base_2.11", version: "2.4.5_0.14.0"
  testCompile group: "org.scalatest", name: "scalatest_2.11", version: "3.0.1"
  testCompile group: "junit", name: "junit", version: "4+"
}
configurations {
  testImplementation.extendsFrom compileOnly
}
```
