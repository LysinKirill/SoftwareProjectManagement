# Спецификация инфраструктуры и развёртывания (SPEC-INFRA)

**ID документа:** SPEC-INFRA  
**Версия:** 1.0  
**Дата:** 11.04.2025  
**Ответственный:** Лысин К.С.

## 1. Область действия
Инфраструктура развёртывания, требования к серверам, контейнеризация, оркестрация, мониторинг и CI/CD пайплайн.

## 2. Связанные требования
- rq-23: Серверные требования (из ТЗ §4.5.1)
- rq-24: Клиентские требования (из ТЗ §4.5.2)

## 3. Критерии приёмки (Acceptance Criteria)

### 3.1. Серверная инфраструктура
**AC-085**: Серверная часть работает на минимальной конфигурации: 4 ядра CPU, 6 ГБ RAM, 30 ГБ SSD.  
**Метод верификации:** VM-081

**AC-086**: Постоянный доступ в интернет со скоростью ≥10 Мбит/сек.  
**Метод верификации:** VM-082

**AC-087**: Поддержка Docker 24+ и Docker Compose 2.20+.  
**Метод верификации:** VM-083

**AC-088**: Возможность горизонтального масштабирования (добавление нод).  
**Метод верификации:** VM-084

### 3.2. Контейнеризация
**AC-089**: Все сервисы упакованы в Docker образы.  
**Метод верификации:** VM-085

**AC-090**: Docker образы публикуются в container registry (GitHub Container Registry или Yandex Container Registry).  
**Метод верификации:** VM-086

**AC-091**: Используются multi-stage builds для уменьшения размера образов.  
**Метод верификации:** VM-087

**AC-092**: Образы сканируются на уязвимости (Trivy, Grype).  
**Метод верификации:** VM-088

### 3.3. Оркестрация
**AC-093**: Развёртывание через Kubernetes (minikube для разработки, Yandex Managed Kubernetes для production).  
**Метод верификации:** VM-089

**AC-094**: Конфигурация через Helm charts или Kustomize.  
**Метод верификации:** VM-090

**AC-095**: Автоматическое масштабирование (HPA) на основе CPU/памяти.  
**Метод верификации:** VM-091

**AC-096**: Ingress controller для маршрутизации трафика.  
**Метод верификации:** VM-092

### 3.4. CI/CD
**AC-097**: Автоматическая сборка при пуше в ветки main/develop.  
**Метод верификации:** VM-093

**AC-098**: Автоматическое тестирование (unit, integration).  
**Метод верификации:** VM-094

**AC-099**: Автоматическое развёртывание в staging окружение.  
**Метод верификации:** VM-095

**AC-100**: Ручное подтверждение для развёртывания в production.  
**Метод верификации:** VM-096

### 3.5. Мониторинг и логирование
**AC-101**: Prometheus для сбора метрик.  
**Метод верификации:** VM-097

**AC-102**: Grafana дашборды для визуализации.  
**Метод верификации:** VM-098

**AC-103**: Loki для сбора логов.  
**Метод верификации:** VM-099

**AC-104**: Alertmanager для оповещений (Telegram, Slack).  
**Метод верификации:** VM-100

### 3.6. Резервное копирование и восстановление
**AC-105**: Ежедневные backup БД (точки восстановления на 30 дней).  
**Метод верификации:** VM-101

**AC-106**: Восстановление из backup занимает ≤1 часа.  
**Метод верификации:** VM-102

**AC-107**: Backup конфигураций и secrets.  
**Метод верификации:** VM-103

### 3.7. Безопасность
**AC-108**: Все secrets хранятся в HashiCorp Vault или Kubernetes Secrets.  
**Метод верификации:** VM-104

**AC-109**: Network policies для изоляции сервисов.  
**Метод верификации:** VM-105

**AC-110**: Регулярные security updates для базовых образов.  
**Метод верификации:** VM-106

## 4. Методы верификации (Verification Methods)

**VM-081**: Проверка конфигурации сервера через системные утилиты.  
**Тип:** Inspection

**VM-082**: Тестирование скорости интернет-соединения.  
**Тип:** Test

**VM-083**: Проверка версий Docker и Docker Compose.  
**Тип:** Inspection

**VM-084**: Тестирование добавления новой ноды в кластер.  
**Тип:** Test

**VM-085**: Проверка Dockerfile и сборка образов.  
**Тип:** Inspection

**VM-086**: Проверка наличия образов в registry.  
**Тип:** Inspection

**VM-087**: Анализ размера Docker образов.  
**Тип:** Analysis

**VM-088**: Сканирование образов на уязвимости.  
**Тип:** Inspection

**VM-089**: Развёртывание на Kubernetes кластере.  
**Тип:** Demo

**VM-090**: Проверка конфигурационных файлов Helm/Kustomize.  
**Тип:** Inspection

**VM-091**: Тестирование горизонтального автомасштабирования.  
**Тип:** Test

**VM-092**: Проверка маршрутизации через Ingress.  
**Тип:** Inspection

**VM-093**: Запуск CI/CD пайплайна при коммите.  
**Тип:** Demo

**VM-094**: Проверка выполнения тестов в CI.  
**Тип:** Inspection

**VM-095**: Автоматическое развёртывание в staging.  
**Тип:** Demo

**VM-096**: Проверка manual approval для production.  
**Тип:** Inspection

**VM-097**: Проверка сбора метрик Prometheus.  
**Тип:** Inspection

**VM-098**: Доступность Grafana дашбордов.  
**Тип:** Inspection

**VM-099**: Проверка сбора логов в Loki.  
**Тип:** Inspection

**VM-100**: Тестирование оповещений через Alertmanager.  
**Тип:** Test

**VM-101**: Проверка создания backup БД.  
**Тип:** Inspection

**VM-102**: Восстановление из backup.  
**Тип:** Test

**VM-103**: Проверка backup конфигураций.  
**Тип:** Inspection

**VM-104**: Проверка хранения secrets.  
**Тип:** Inspection

**VM-105**: Проверка network policies.  
**Тип:** Inspection

**VM-106**: Проверка обновлений базовых образов.  
**Тип:** Inspection

## 5. Технические детали

### 5.1. Архитектура развёртывания
```
Kubernetes Cluster (Yandex Cloud)
├── Namespace: personage-production
│ ├── Deployment: api-service (3 реплики)
│ ├── Deployment: auth-service (2 реплики)
│ ├── Deployment: processor-service (2 реплики)
│ ├── StatefulSet: postgres (1 мастер, 2 реплики)
│ ├── StatefulSet: redis (кластер 3 ноды)
│ └── Deployment: kafka (3 брокера)
└── Monitoring Stack
├── Prometheus
├── Grafana
└── Loki
```

### 5.2. Требования к ресурсам (production)
```yaml
api-service:
  requests:
    cpu: "500m"
    memory: "512Mi"
  limits:
    cpu: "1000m"
    memory: "1024Mi"

auth-service:
  requests:
    cpu: "300m"
    memory: "256Mi"
  limits:
    cpu: "500m"
    memory: "512Mi"

postgres:
  storage: "50Gi"
  requests:
    cpu: "1000m"
    memory: "2048Mi"

redis:
  storage: "10Gi"
  requests:
    cpu: "500m"
    memory: "1024Mi"
```

### 5.3. CI/CD Pipeline (GitHub Actions)
```yaml
name: CI/CD Pipeline
on:
  push:
    branches: [main, develop]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: dotnet test

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Build Docker images
        run: docker-compose build

  deploy-staging:
    needs: build
    if: github.ref == 'refs/heads/develop'
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to staging
        run: kubectl apply -f k8s/staging/

  deploy-production:
    needs: build
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - name: Wait for manual approval
        uses: trstringer/manual-approval@v1
      - name: Deploy to production
        run: kubectl apply -f k8s/production/
```

### 5.4. Мониторинг - ключевые метрики
#### Application metrics
```
- personage_api_request_duration_seconds
- personage_api_requests_total
- personage_db_connections_active
- personage_cache_hit_ratio
```
#### Infrastructure metrics
```
- container_cpu_usage_seconds_total
- container_memory_usage_bytes
- kafka_topic_messages_per_second
- postgresql_connections
```
### Business metrics
```
- personage_users_active_total
- personage_events_processed_total
- personage_llm_requests_total
```

### 5.5. Алерт правила (пример)
```yaml
groups:
  - name: personage-alerts
    rules:
    - alert: HighAPIErrorRate
      expr: rate(personage_api_errors_total[5m]) > 0.1
      for: 5m
      annotations:
        summary: "High API error rate"

    - alert: DatabaseDown
      expr: up{job="postgres"} == 0
      for: 1m
      annotations:
        summary: "Database is down"

    - alert: HighMemoryUsage
      expr: container_memory_usage_bytes / container_spec_memory_limit_bytes > 0.8
      for: 5m
      annotations:
        summary: "Container memory usage high"
```

### 5.6. Резервное копирование
#### Daily PostgreSQL backup
```bash
pg_dump -h postgres -U personage personage_db | gzip > /backups/personage_$(date +%Y%m%d).sql.gz
```
#### Retention: 30 days
```bash
find /backups -name "*.sql.gz" -mtime +30 -delete
```
#### Restore procedure
```bash
gunzip < backup_file.sql.gz | psql -h postgres -U personage personage_db
```