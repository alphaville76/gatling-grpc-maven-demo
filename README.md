# Gatling-gRPC demo in Maven

A demo project showcasing a Gatling test
living in the same project as the gRPC server.

## Run

Run the server: `./mvnw compile exec:java`\
Run the load test: `./mvnw gatling:test`


## Dynamic Payload

This project also demonstrates the integration between
Java Protobuf messages with Gatling Expressions.

```scala
val message: Expression[Ping] =
  Ping.getDefaultInstance
    // dynamic payload!
    .update(_.setData)($("data"))
```

`_.setData` is a method reference of `Ping.Builder`; and\
`data` is a [session attribute](https://gatling.io/docs/current/session/session_api/)
containing a number.

See the runtime-generated payload in the `TRACE` logging!

```
=========================
gRPC request:
headers=
grpc-accept-encoding: gzip
payload=
data: 18

=========================
gRPC response:
status=
OK
body=
data: 18

<<<<<<<<<<<<<<<<<<<<<<<<<
```
