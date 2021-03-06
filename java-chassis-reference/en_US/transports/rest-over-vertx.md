# REST over Vertx

## Configuration

The REST over Vertx communication channel runs in standalone mode, it can be started in the main function. In the main function, you need to initialize logs and load service configuration. The code is as follow:

```java
import org.apache.servicecomb.foundation.common.utils.BeanUtils;
import org.apache.servicecomb.foundation.common.utils.Log4jUtils;

public class MainServer {
  public static void main(String[] args) throws Exception {
  　Log4jUtils.init();// Log initialization
  　BeanUtils.init(); // Spring bean initialization
  }
}
```

To use the REST over Vertx communication channel, add the following dependencies in the maven pom.xml file:

```xml
<dependency>
　　<groupId>org.apache.servicecomb</groupId>
　　<artifactId>transport-rest-vertx</artifactId>
</dependency>
```

The REST over Vertx related configuration items in the microservice.yaml file are described as follows:

Table 1-1 Configuration items for REST over Vertx

| Configuration Item                                     | Default Value                                  | Description                                    |
| :----------------------------------------------------- | :--------------------------------------------- | :--------------------------------------------- |
|servicecomb.rest.address                                |                                                |listening address, empty for not listen, just a rest client |
|servicecomb.rest.server.connection-limit                |Integer.MAX_VALUE                               |Max allowed client connections                  | 
|servicecomb.rest.server.thread-count                    |[verticle-count](/transports/verticle-count.md) |rest server verticle instance count(Deprecated) |
|servicecomb.rest.server.verticle-count                  |[verticle-count](/transports/verticle-count.md) |rest server verticle instance count             |
|servicecomb.rest.server.connection.idleTimeoutInSeconds |60                                              |Timeout for server's idle connection, The idle connections will be closed |
|servicecomb.rest.client.thread-count                    |[verticle-count](/transports/verticle-count.md) |rest client verticle instance count(Deprecated) |
|servicecomb.rest.client.verticle-count                  |[verticle-count](/transports/verticle-count.md) |rest client verticle instance count             |
|servicecomb.rest.client.connection.maxPoolSize          |5                                               |The maximum number of connections in each connection pool for an IP:port combination |
|servicecomb.rest.client.connection.idleTimeoutInSeconds |30                                              |Timeout for client's idle connection, The idle connections will be closed |
|servicecomb.rest.client.connection.keepAlive            |true                                            |Whether to use long connections                 |

## Sample Code

An example of the configuration in the microservice.yaml file for REST over Vertx:

```yaml
servicecomb:
  rest:
    address: 0.0.0.0:8080
    thread-count: 1
  references:
    hello:
      transport: rest
      version-rule: 0.0.1
```

