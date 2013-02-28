## Nettosphere: A Java WebSocket and HTTP server powered by the [Atmosphere Framework](http://github.com/Atmosphere/atmosphere) and the [Netty Framework](http://netty.io/)

The easiest way to get started with NettoSphere is to download a sample and start it. [Or look at the Javadoc](http://atmosphere.github.com/nettosphere/apidocs/). You can download the [Chat](http://search.maven.org/remotecontent?filepath=org/atmosphere/nettosphere/samples/nettosphere-chat/1.4.2/nettosphere-chat-1.4.2-distribution.zip) or [Jersey](http://search.maven.org/remotecontent?filepath=org/atmosphere/nettosphere/samples/nettosphere-jersey-chat/1.4.2/nettosphere-jersey-chat-1.4.2-distribution.zip) distribution.

```bash
   % unzip nettosphere-<name>-distribution.jar
   % chmod a+x ./bin/nettosphere.sh
   % ./bin/nettosphere.sh
```

Samples are the same as then one available in Atmosphere. Bootstrap classes looks like [AtmosphereHandler](https://github.com/Atmosphere/nettosphere/blob/master/samples/chat/src/main/java/org/nettosphere/samples/chat/NettosphereChat.java#L27) or [Jersey](https://github.com/Atmosphere/nettosphere/blob/master/samples/jersey-chat/src/main/java/org/nettosphere/samples/chat/NettosphereJerseyChat.java#L31)

Download Nettosphere [here](https://oss.sonatype.org/content/repositories/snapshots/org/atmosphere/nettosphere/1.4.2/) or use Maven

```xml
     <dependency>
         <groupId>org.atmosphere</groupId>
         <artifactId>nettosphere</artifactId>
         <version>1.4.2</version>
     </dependency>
```

or test out upcoming release, which is powered by Atmosphere 1.1.0

```xml
     <dependency>
         <groupId>org.atmosphere</groupId>
         <artifactId>nettosphere</artifactId>
         <version>2.0.0.beta1</version>
     </dependency>
```

### Super Simple Web Application

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .resource(new Handler() {
                        void handle(AtmosphereResource r) {
                            r.getResponse().write("Hello World").write("from Nettosphere").flush();
                        }
                    })
                    .build())
                 .build();
    server.start();
```

All [Atmosphere](http://jfarcand.wordpress.com/2011/11/07/hitchiker-guide-to-the-atmosphere-framework-using-websocket-long-polling-and-http-streaming/) API supported. As simple as:

[Top](#Top)

### Server static and dynamic resources, use atmosphere.xml to configure NettoSphere

```java
        Config.Builder b = new Config.Builder();
        b.resource("./webapps")
            .port(8080)
            .host("127.0.0.1")
            .configFile("../conf/atmosphere.xml")
            .build();
        Nettosphere s = new Nettosphere.Builder().config(b.build()).build();
```
[Top](#Top)

### Deploy a Resource (annotated using Jersey), access it using HTTP or WebSocket

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .resource(MyResource.class)
                    .build())
                 .build();
    server.start();
```
[Top](#Top)

### Deploy an AtmosphereHandler, access it using HTTP or WebSocket

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .resource("/*", MyAtmosphereHandler.class)
                    .build())
                 .build();
    server.start();
```

### Deploy an AtmosphereHandler, define a WebSocket protocol

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .webSocketProtocol(JMSOverWebSocketProtocol.class)
                    .resource("/*", MyAtmosphereHandler.class)
                    .build())
                 .build();
    server.start();
```
[Top](#Top)

### Deploy a Servlet which use Meteor

```java
    Nettosphere server = new Nettosphere.Builder().config(
                 new Config.Builder()
                    .host("127.0.0.1")
                    .port(8080)
                    .resource("/*", MyServlet.class)
                    .build())
                 .build();
    server.start();
```
[Top](#Top)

### The Server can also be started using java

```java
    java -cp nettosphere-all.jar
          org.atmosphere.nettosphere.Nettosphere
                [/path/to/an/exploded/war/file] [host] [port]
```
[Top](#Top)

### Using Maven and the Git repo

    mvn exec:java -Dexec.arguments='path to your exploded war file'

We are on irc.freenode.net under #atmosphere-comet and [Twitter](http://twitter.com/jfarcand)
