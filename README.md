Twitter for PlayFramework
=========================

 - [Fizzed, Inc.](http://fizzed.com)
 - Joe Lauer (Twitter: [@jjlauer](http://twitter.com/jjlauer))


## Overview

[Play Framework](http://www.playframework.org/) 2.x. to fetch, cache, and display
tweets from Twitter. Resilient against Twitter API downtime by maintaining a cached
copy of the last successful API call. Basic rendering of tweets into html for simple
display -- or using the advanced object model to render your own.


## Compatibility matrix

| PlayFramework version | Module version | 
|:----------------------|:---------------|
| 2.3.x                 | 2.2.0          |
| 2.2.x                 | 2.1.0          |
| 2.1.x                 | 2.0.1          |


## Usage

This module is published to Maven Central.  You will need to include the module in your
dependencies list, in `build.sbt` or `Build.scala` file:


### build.sbt

```scala
libraryDependencies ++= Seq(
  "com.fizzed" %% "fizzed-play-module-twitter" % "2.2.0"
)
```

### Build.scala

```scala
import sbt._
import Keys._
import play.Project._

object ApplicationBuild extends Build {

  val appName         = "sample"
  val appVersion      = "1.0-SNAPSHOT"

  val appDependencies = Seq(
    javaCore,
    javaJdbc,
    javaEbean,
    "com.fizzed" %% "fizzed-play-module-twitter" % "2.2.0"
  )
  
  ...
}
```


## Configuration

### conf/play.plugins

Create this configuration file if it doesn't exist. Add this line to activate
the plugin at runtime.

`1000:com.fizzed.play.twitter.TwitterPlugin`

### conf/application.conf

```
twitter.access-token = "required: replace with twitter access token"
twitter.access-secret =  "required: replace with twitter access secret"
twitter.consumer-key = "required: replace with twitter consumer key"
twitter.consumer-secret = "required: replace with twitter consumer secret"
twitter.refresh-interval = 60m
```

### From a Java-based controller

See [fizzed-java-sample](https://github.com/fizzed/play-module-twitter/tree/master/sample/fizzed-java-sample) project for full example.

```java
package controllers;

import com.fizzed.play.twitter.TwitterPlugin;

import play.*;
import play.mvc.*;

public class Application extends Controller {
  
    static public TwitterPlugin TWITTER_PLUGIN = Play.application().plugin(TwitterPlugin.class);
	
    public static Result index() {
        return ok(views.html.index.render());
    }
    
    public static TwitterPlugin twitter() {
    	return TWITTER_PLUGIN;
    }
  
}
```

### From a Scala-based controller

See [fizzed-scala-sample](https://github.com/fizzed/play-module-twitter/tree/master/sample/fizzed-scala-sample) project for full example.

```scala
package controllers

import com.fizzed.play.twitter.TwitterPlugin

import play.api._
import play.api.mvc._

object Application extends Controller {

  val TWITTER_PLUGIN = Play.current.plugin[TwitterPlugin]

  def index = Action {
    Ok(views.html.index("Fizzed Twitter Module Sample"))
  }

}
```
