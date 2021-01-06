# Tokenize for Java (and any JVM-based language)
[![License](https://img.shields.io/github/license/vinceh121/tokenize4j.svg?style=flat-square)](https://github.com/vinceh121/tokenize4j/blob/master/LICENSE)
[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/vinceh121/tokenize4j/Java%20CI%20with%20Maven?style=flat-square)](https://github.com/vinceh121/tokenize4j/actions?query=workflow%3A%22Java+CI+with+Maven%22)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/vinceh121/tokenize4j?style=flat-square)](https://github.com/vinceh121/tokenize4j/releases)

## Installation

With Gradle:
```groovy
repositories {
  maven { url 'https://jitpack.io' }
}
dependencies {
  implementation 'com.github.vinceh121:tokenize4j:...'
}
```

With Maven:
```xml
<repositories>
  <repository>
    <id>jitpack.io</id>
    <url>https://jitpack.io</url>
  </repository>
</repositories>
<dependency>
  <groupId>com.github.vinceh121</groupId>
  <artifactId>tokenize4j</artifactId>
  <version>...</version>
</dependency>
```

## How to use it
```java
public class Main {
    public static void main(String[] args) {
        Tokenize tokenize = new Tokenize("very secure private key".getBytes());

        // Generation
        Token token = tokenize.generateToken(account);
        System.out.println(token); // xxxxxxxx.xxxxxxxxxxx.xxxxxxxxx

        // Validation
        String rawToken = "xxxxxxxx.xxxxxxxxxxx.xxxxxxxxx";
        Token token;
        try {
            token = tokenize.validateToken(rawToken, id -> Database.fetchAccount(id));
        } catch (SecurityException e) {
            System.out.println("Invalid token signature!");
        }
    }
}
```

## License
This implementation is licensed under the BSD-3-Clause license.

