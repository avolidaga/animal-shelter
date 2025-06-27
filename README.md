## Local development (Linux/WSL/macOS only)

### Run via docker

build App + run App and PostgresqlDB:
```sh
gradle jibDockerBuild 
docker compose up
```

### Run DB in docker and App in IDE

run only db in docker:
```sh
docker-compose up db
```


## Liquibase

Для написания файлов миграций используется YAML.

Структура:

```
- resources:
  - db:
    - changelog-root.yaml
    - changelog:
      - changelog-1.0:
        - tables.yaml
        - procedures.yaml
        - ...
      - changelog-1.1:
        - tables.yaml
        - procedures.yaml
      - ...
```

## Kafka

Просмотр лидера кластера
```bash
docker compose exec kafka-1 kafka-metadata-shell.sh \
  --snapshot /bitnami/kafka/data/__cluster_metadata-0/00000000000000000000.log \
  cat /metadataQuorum/leader
```

Проверка доступности данных на другой реплике
```bash
docker compose exec kafka-2 bash
$ kafka-console-consumer.sh --topic events --bootstrap-server localhost:9092 --from-beginning
```

## Тестирование на стенде

Swagger находится по адрессу 
```
http://89.169.185.177:8080/webjars/swagger-ui/index.html
```

Тестовый пользователь
```json
{
  "login": "customer",
  "password": "1234"
}
```

Тестовый админ
```json
{
  "login": "amanager",
  "password": "1234"
}
```


