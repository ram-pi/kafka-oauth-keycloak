# Kafka OAuth with Keycloak example

## Start

```
docker-compose up -d
```

## Check OAuth Compatibility

```
kafka-run-class org.apache.kafka.tools.OAuthCompatibilityTool \
  --clientId kafka-client \
  --clientSecret b2p9lOBr32CGgehJR22KXpq6DcNmiaUt \
  --sasl.oauthbearer.token.endpoint.url http://localhost:8080/realms/kafka/protocol/openid-connect/token \
  --sasl.oauthbearer.jwks.endpoint.url http://localhost:8080/realms/kafka/protocol/openid-connect/certs
```

## OAuth Client

```
kafka-topics --bootstrap-server localhost:9093 --command-config client.properties --list
```

## Utils

### Export Keycloak Realm

```
docker exec -it keycloak bash
cd /opt/keycloak
./kc.sh export --dir ~/
exit
docker cp keycloak:/opt/keycloak/kafka-realm.json ./realms/kafka-realm.json
```
