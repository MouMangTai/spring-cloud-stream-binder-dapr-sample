# Spring cloud stream binder for dapr samples

This is a publish sample of usage of a Spring Cloud Stream Binder Dapr.

## QuickStart

### 1. Build binder project
Clone [Binder project](https://github.com/MouMangTai/spring-cloud-stream-binder-dapr) and install the *com.azure.spring.cloud.stream.binder.dapr* artifact in your local repository by moving to the main project folder and running:
   `mvn clean install`

Move back to the sample project,
you will find that the `External Libraries`
includes `com.azure.spring:spring-cloud-stream-binder-dapr:1.0-SNAPSHOT` dependency,
that means the sample project already depends on our binder.
### 2. Run Message Subscriber app with Dapr
```
cd subscriber
dapr run --app-id subscriber --app-port 9090 --components-path ../components  --app-protocol grpc --dapr-grpc-port 50001 mvn spring-boot:run
```

You can simply just run dapr, but you won't see the printout.
```
dapr run --app-id subscriber --app-port 9090 --components-path ../components  --app-protocol grpc --dapr-grpc-port 50001
```
> **Note:**
> If you already have a message subscriber application running through dapr and meet the requirements in Pre-requisites, you can skip this step.
>
> **Note:**
> You also could refer to [here](https://github.com/dapr/quickstarts/tree/master/pub_sub/java/sdk#run-java-message-subscriber-app-with-dapr) to run Java message subscriber app with Dapr.

#### Pre-requisites

- Message subscriber App with Dapr with the following properties
    - The protocol Dapr uses to talk to the application: **Grpc**
    - The gRPC port for Dapr to listen on: **50001**
    - Dapr component name: **"pubsub"**
    - Topic name: **"topic"**
### 3. Run Message Publisher app which depend on Dapr binder
```
cd publisher
mvn spring-boot:run
```

### 4. Output

```
# publisher
Sending message, sequence 0
Sending message, sequence 1
Sending message, sequence 2
Sending message, sequence 3
Sending message, sequence 4
...

# subscriber
------onTopicEvent------
TopicEventRequest :
id: "34e3efdb-20bc-4551-83bf-432049e6b1f9"
source: "subscriber"
type: "com.dapr.event.sent"
spec_version: "1.0"
data_content_type: "text/plain"
topic: "topic"
data: "\"SGVsbG8gd29ybGQsIDEx\""
pubsub_name: "pubsub"
...
```
