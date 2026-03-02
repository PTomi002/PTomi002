## Kafka 101

### Authentication Types

#### Mutual TLS

This is a mutual TLS solution works in a way:
- Client uses it's truststore to check the kafka broker's identity with it.
- The broker asks for the client's certificate from it's keystore to verify it's identity.

```
security.protocol=SSL

ssl.keystore.location=kafka.client.keystore.jks
ssl.keystore.password=keystore-password
ssl.key.password=key-password

ssl.truststore.location=kafka.client.truststore.jks
ssl.truststore.password=truststore-password
```

#### SSL - SASL - SCRAM

SASL is a framework that allows Kafka to use various "pluggable" authentication methods.

Works in a way:
- (Optional) Client uses it's truststore to check the kafka broker's identity with it.
- Client provides it's username + password.
- The password is hashed with a salt, the actual password never sent over the wire.

```
security.protocol=SASL_SSL
sasl.mechanism=SCRAM-SHA-512

sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required \
    username="my-kafka-user" \
    password="my-secret-password";

----- Optional ----- 
ssl.truststore.location=kafka.client.truststore.jks
ssl.truststore.password=truststore-password
```

#### SSL - SASL - Plain Text

Works in a way:
- (Optional) Client uses it's truststore to check the kafka broker's identity with it.
- Client provides it's username + password.


```
security.protocol=SASL_SSL
sasl.mechanism=PLAIN

sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
username="my-kafka-user" \
password="my-secret-password";

----- Optional -----
ssl.truststore.location=kafka.client.truststore.jks
ssl.truststore.password=truststore-password
```

### HOW-TO: Rotate Password

1. Set the new password for the user at the kafka broker side.
2. Do the following changes parallel:
   1. Restart the kafka broker service to have effect on the new password.
   2. Update the Key Vaults to contain the new password.
3. Restart the applications to fetch the new password.
4. Validate the connections by inspecting the application logs.
