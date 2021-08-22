## Running the sample code

1. Start a first node:

```shell
sbt -Dconfig.resource=local1.conf run
```

2. (Optional) Start another node with different ports:

```shell
sbt -Dconfig.resource=local2.conf run
```

3. Check for service readiness

```shell
curl http://localhost:9101/ready
```

## link

* [Implementing Microservices with Akka](https://developer.lightbend.com/docs/akka-platform-guide/microservices-tutorial/index.html)

## docker

```shell
docker-compose up -d
docker exec -i shopping-cart-service_postgres-db_1 psql -U shopping-cart -t < ddl-scripts/create_tables.sql
```

## docker publish to aws

下記コマンドを IntelliJ の configurationに入れておくと楽かも

```shell
# aws ecr login
aws ecr get-login-password --region ap-northeast-1 | docker login --usernameAWS --password-stdin <aws account id>.dkr.ecr.ap-northeast-1.amazonaws.com
# docker publish to aws ecr
sbt -Ddocker.registry=<aws account id>.dkr.ecr.ap-northeast-1.amazonaws.com docker:publish
```