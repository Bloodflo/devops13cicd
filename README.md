# DevOps Lab 13: CI/CD Pipeline

## Описание
Репозиторий содержит пример приложения на Python с настроенным полным циклом CI/CD/GitOps.

## Структура проекта
devops13cicd/
├── .github/workflows/
│ ├── cicd.yml # CI пайплайн (lint, test, build)
│ └── release.yml # CD пайплайн (build, push)
├── server/
│ ├── application.py # Исходный код приложения
│ ├── test_application.py # Юнит-тесты
│ └── dockerfile # Docker образ
├── server-k8s-manifests/
│ └── devops-psu.yml # Kubernetes манифесты
├── screenshots/ # Скриншоты выполнения
├── requirements.txt # Python зависимости
└── README.md # Этот файл


## Как это работает

### CI (Continuous Integration)
1. Разработчик пушит код в ветку `dev`
2. GitHub Actions запускает проверки:
   - **lint** — проверка кода через pylint
   - **unit-tests** — запуск pytest
   - **build-test** — сборка и тест Docker образа

### CD (Continuous Delivery)
1. После мержа в `master` запускается release пайплайн
2. Образ собирается и пушится в Docker Hub
3. Манифест обновляется и пушится в ветку `release`

### GitOps (ArgoCD)
1. ArgoCD отслеживает ветку `release`
2. При изменениях автоматически синхронизирует кластер
3. Приложение обновляется без участия человека

## Скриншоты
Все скриншоты успешного выполнения находятся в папке `screenshots/`

## Автор
Blodflo
