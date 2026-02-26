## Kafka 101

### Authentication Types

#### SSL + TrustStore

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

#### SASL - SCRAM

SASL is a framework that allows Kafka to use various "pluggable" authentication methods.

Works in a way:
- (Optional) Client uses it's truststore to check the kafka broker's identity with it.
- Client provides it's username + password.

```
security.protocol=SASL_SSL
sasl.mechanism=SCRAM-SHA-512

sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required \
    username="my-kafka-user" \
    password="my-secret-password";

ssl.truststore.location=kafka.client.truststore.jks
ssl.truststore.password=truststore-password
```

### HOW-TO: Rotate Password

1. Prepare or Set the new password in Azure Key Vault.
2. Set the new password on the kafka broker (the same time as Step 1).
3. Restart the applications to fetch the new password.
