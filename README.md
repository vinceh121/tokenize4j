# Tokenize for Java (and any JVM-based language)
[![License](https://img.shields.io/github/license/vinceh121/tokenize4j.svg?style=flat-square)](https://github.com/vinceh121/tokenize4j/blob/master/LICENSE)
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
    public static void main(final String[] args) {
        final Tokenize tokenize = new Tokenize("very secure private key".getBytes());

        // Generation
        final Token token = tokenize.generateToken(account);
        System.out.println(token); // xxxxxxxx.xxxxxxxxxxx.xxxxxxxxx

        // Validation
        String rawToken = "xxxxxxxx.xxxxxxxxxxx.xxxxxxxxx";
        Token token;
        try {
            token = tokenize.validateToken(rawToken, id -> Database.fetchAccount(id));
        } catch (final SecurityException e) {
            System.out.println("Invalid token signature!");
        }

        // Get an OTP key
        final OTPKey key = OTPKey.builder().name("Key Name").issuer("Issuer name").build();
        System.out.println(key.getKey()); // You just need to store this in your database
        System.out.println(key.getGoogleURI()); // Throw this in a QR code

        // Validate an OTP code
        System.out.println(OTPUtils.validateTotp("013370", "xxxxxxxxxxxxxxxx"));
        System.out.println(OTPUtils.validateHotp("013370", "xxxxxxxxxxxxxxxx", 1));
    }
}
```

## License
This implementation is licensed under the BSD-3-Clause license.

