# Java SDK for Satori RTM
![Maven Central](https://img.shields.io/maven-central/v/com.satori/satori-rtm-sdk.svg)

Use the Java SDK for the Satori RTM to create server-based or mobile Android
 applications that use the RTM to publish and subscribe.

# Installing the Java SDK

## Maven

To install the Java SDK from the Central Maven repository using Maven, add the following lines to `pom.xml`:

```
<dependency>
    <groupId>com.satori</groupId>
    <artifactId>satori-rtm-sdk</artifactId>
    <version>1.0.3</version>
</dependency>
```

## Gradle

To install the Java SDK from the Central Maven repository using Gradle, add the following lines to `build.gradle`:

```
dependencies {
    compile group: 'com.satori', name: 'satori-rtm-sdk', version:'1.0.3'
}
```

# Documentation

The various documentation is available:

* The [Java SDK page on Satori Website](https://www.satori.com/docs/client-libraries/java).
* The [JavaDoc](https://satori-com.github.io/satori-rtm-sdk-java/).
* The [RTM API](https://www.satori.com/docs/references/rtm-api) specification.

# Logging

The Java SDK uses slf4j library as an abstraction for various logging frameworks. We have not provided any back-end implementation.
Choose an implementation that applies to your project.

For more information, see the [slf4j](https://www.slf4j.org/) documentation.

# JSON Library

Satori Java SDK could work with different JSON libraries. By default, Java SDK uses the [google-gson](https://github.com/google/gson) library for JSON serialization.

You can specify your own serialization module in `ClientBuilder` to use a different JSON library.

Satori Java SDK has adapter to use [Jackson2](http://wiki.fasterxml.com/JacksonHome) library. To use it use assembly with Jackson2 support.

```
dependencies {
    compile group: 'com.satori', name: 'satori-rtm-sdk-jackson2', version:'1.0.3'
}
```

# Using HTTPS proxy

The SDK supports working through an HTTPS proxy.

The following is an example how to set a proxy server:

```Java
RtmClient client = new RtmClientBuilder("YOUR_ENDPOINT", "YOUR_APPKEY")
    .setHttpsProxy(URI.create("http://127.0.0.1:3128"))
    .build();
```

# Running Tests

Tests require an active RTM to be available. The tests require `credentials.json` to be
populated with the RTM properties.

The `credentials.json` file must include the following key-value pairs:

```
{
  "endpoint": "wss://<SATORI_HOST>/",
  "appkey": "<APP_KEY>",
  "auth_role_name": "<ROLE_NAME>",
  "auth_role_secret_key": "<ROLE_SECRET_KEY>",
  "auth_restricted_channel": "<CHANNEL_NAME>"
}
```

* `endpoint` is your customer-specific DNS name for RTM access.
* `appkey` is your application key.
* `auth_role_name` is a role name that permits to publish / subscribe to `auth_restricted_channel`. Must be not `default`.
* `auth_role_secret_key` is a secret key for `auth_role_name`.
* `auth_restricted_channel` is a channel with subscribe and publish access for `auth_role_name` role only.

You must use [DevPortal](https://developer.satori.com/) to create role and set channel permissions.

After setting up `credentials.json`, run SDK tests with the following commands:

```
./gradlew test -DRTM_CONFIG=./credentials.json
```

If the `RTM_CONFIG` option is not specified, the SDK uses `<SDK ROOT>/credentials.json`.
