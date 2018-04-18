---
layout: page
title: "Setting up"
category: use
order: 1
date: 2017-03-03 09:26:50
js:
- deps/mavenrepo.js
---

1. TOC
{:toc}

### What you should know

Kweb is built on [Kotlin 1.1](http://kotlinlang.org/), you should have some familiarity to Kotlin
and the Java ecosystem on which it's built.

### Adding a Kweb dependency

The Kweb library is distributed via [JitPack](https://jitpack.io/#sanity/kweb), it can be added
easily to any Kotlin project:

#### Gradle 
For [Gradle](http://www.gradle.org/) users, add this to the repositories section of your `build.gradle`:
```groovy
  repositories {
    // ...
    maven { url 'https://jitpack.io' }
    maven {url "https://kotlin.bintray.com/ktor"}
    }
```

Then add this to the dependencies section of your `build.gradle`:
```groovy
dependencies {
  // ...
  compile 'com.github.kwebio:kweb:MAVEN_VERSION_PLACEHOLDER'
  compile 'org.slf4j:slf4j-simple:1.6.1' // <-- or your favorite SLF4J logger binding 
}
```

#### Kobalt

For [Kobalt](http://beust.com/kobalt/) users, add this to your `Built.kt` file:

```kotlin
  buildScript {
    // ...
    repos(
        "https://jitpack.io", 
        "http://dl.bintray.com/kotlin/kotlin-eap-1.1", 
        "http://dl.bintray.com/kotlin/ktor"
        )
    // ...
  }
```

```kotlin
  dependencies {
    // ...
    compile("com.github.kwebio:kweb:MAVEN_VERSION_PLACEHOLDER")
    compile("org.slf4j:slf4j-simple:1.6.1") // <-- or your favorite SLF4J logger binding 
    // ...
  }
```

#### Maven
For [Maven](https://maven.apache.org/) users, add this to the repositories section of your `pom.xml`:
```xml
<repositories>
<repository><id>jitpack.io</id><url>https://jitpack.io</url></repository>
<repository><snapshots><enabled>false</enabled></snapshots>
    <id>dl</id><name>bintray</name><url>http://dl.bintray.com/kotlin/kotlin-eap-1.1</url>
</repository>
<repository><id>ktor</id><url>http://dl.bintray.com/kotlin/ktor</url></repository>
</repositories>
```

Then add this to the dependencies section of your `pom.xml`:
```xml
<dependency>
  <groupId>com.github.kwebio</groupId>
  <artifactId>kweb</artifactId>
  <version>MAVEN_VERSION_PLACEHOLDER</version>
</dependency>  

<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId> <!-- or your favorite SLF4J logger binding -->
    <version>1.6.1</version>
</dependency>
```

### Logging
Kweb uses [SLF4J](https://www.slf4j.org/) for logging.  This is a "logging facade", it allows
libraries to log to the library user's preferred logging framework.  The instructions above 
include the "simple" SLF4J logger binding, but you can replace this to a number of others, 
depending on your needs or preferences, learn more 
[here](http://saltnlight5.blogspot.com/2013/08/how-to-configure-slf4j-to-different.html).

If you see an error like the following:
```
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
```

...it means that you have not provided an SLF4J logging implementation.  This is undesirable because
Kweb provides some useful warnings that you won't see without this.

-----------

**Next: [Your First Kwebsite]({{ site.baseurl }}{% post_url 2017-03-08-your-first-kwebsite %}) >>>>**
