# Ollama + Open WebUI

Локальный чат с LLM (Llama и др.) через веб-интерфейс. Всё в Docker.

## Что нужно

- [Docker](https://docs.docker.com/get-docker/) и Docker Compose

## Запуск

```bash
git clone https://github.com/IllKA8/Ai_ubu.git
cd Ai_ubu
docker compose up -d
```

Откройте в браузере: **http://localhost:3000**

При первом заходе создайте аккаунт. Моделей по умолчанию нет — скачайте одну командой:

```bash
docker exec -it ollama ollama pull llama3.2:3b
```

После загрузки обновите страницу и выберите модель в интерфейсе. [Список моделей Ollama](https://ollama.com/library).

## Остановка

```bash
docker compose down
```

Данные и модели хранятся в томах Docker и не удалятся.

## Продакшен (сервер)

Создайте `.env`, задайте `WEBUI_SECRET_KEY` либо например, openssl rand -hex 32, если не создался автоматически. При необходимости закройте порты фаерволом и поставьте HTTPS (Nginx/Caddy) перед Open WebUI.
