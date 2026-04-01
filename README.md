# Library Workspace

Корневой workspace для сервиса `document_description` и его Docker-окружения.

## Что внутри

- `docker-compose.yml` — запуск PostgreSQL + `document_description`,
- `document_description/` — NestJS API (Swagger, миграции, сиды, e2e/unit тесты)

## установка с Git 
```bash
git clone --recurse-submodules git@github.com:AlexSokolskih/library_test_task_postgres.git
```
скачает основной репозиторий + вложенные репозитории (submodules)

Если склонировал без submodule
Тогда : 
git submodule update --init --recursive

 
## Быстрый старт (Docker)

```bash
cd library_test_task_postgres/
docker compose up -d --build
```
#запускаем тесты
```bash
docker compose exec document_description npm run test:all
```



## Доступы и порты 

- API: `http://localhost:3000`
- Swagger: `http://localhost:3000/api/docs`
- Postgres (host mode): `127.0.0.1:5433`
- Bearer token (по умолчанию в compose): `change-me`


## API smoke-check

```bash
curl -i http://localhost:3000/api/docs

curl -i \
  -H "Authorization: Bearer change-me" \
  "http://localhost:3000/document-descriptions?page=1&per_page=2"
```

## Документация сервиса

Детальная документация по эндпоинтам и архитектуре:

- [document_description/README.md](https://github.com/AlexSokolskih/library_test_task_main/blob/main/README.md)

## CI (GitHub Actions)

При каждом `push` и `pull_request` запускается workflow `Tests`:

- файл: `.github/workflows/tests.yml`
- шаги: `npm ci` и `npm test -- --runInBand` в `document_description`
- где смотреть статус: вкладка `Actions` в GitHub репозитории
