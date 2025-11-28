# Observability Stack Template

Prometheus + Grafana + Exporters(MySQL, Redis, RabbitMQ, Elasticsearch) 템플릿.

## 사용법

1. `.env` 설정

```bash
cp .env.example .env
# 값 수정 (MySQL 계정, Redis 주소, RabbitMQ 계정 등)
````

2. 앱 네트워크 연결

* 기존 애플리케이션 docker-compose에서 `OBS_DOCKER_NETWORK`와 동일한 이름의 external 네트워크를 사용하도록 설정

예:

```yaml
networks:
  papyrus-app:
    external: true
```

3. 필요한 프로필만 선택해서 띄우기

* MySQL + Redis만 모니터링:

```bash
docker compose --profile mysql --profile redis up -d
```

* 전체:

```bash
docker compose --profile node --profile mysql --profile redis --profile rabbitmq --profile es up -d
```

4. 접속

* Prometheus: `http://<host>:9090`
* Grafana: `http://<host>:3000` (기본 admin/admin → `.env`에서 변경 가능)

5. Dashboards

* Grafana → Dashboards → Import

  * MySQL / Redis / RabbitMQ / Elasticsearch / Spring Boot 템플릿 ID 사용
