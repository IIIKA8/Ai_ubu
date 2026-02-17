# Ollama + Open WebUI

Локальный чат с LLM (Llama и др.) через веб-интерфейс. Два варианта: полный стек в Docker или только веб-интерфейс к уже установленной Ollama.

## Что нужно

- [Docker](https://docs.docker.com/get-docker/) и Docker Compose

---

## Вариант 1: Всё в Docker (Ollama + Open WebUI)

Подходит для чистого сервера или ПК — поднимаются оба контейнера, модели качаются отдельно.

```bash
git clone https://github.com/IllKA8/Ai_ubu.git
cd Ai_ubu
docker compose up -d
```

Откройте в браузере: **http://localhost:3000**

Моделей по умолчанию нет — скачайте одну командой:

```bash
docker exec -it ollama ollama pull llama3.2:3b
```

После загрузки обновите страницу и выберите модель. [Список моделей Ollama](https://ollama.com/library).

**Остановка:** `docker compose down`

---

## Вариант 2: Только Open WebUI (Ollama уже на сервере)

Если Ollama установлена напрямую на хост и модели уже скачаны — поднимается только веб-интерфейс, он подключается к хостовой Ollama.

```bash
git clone https://github.com/IllKA8/Ai_ubu.git
cd Ai_ubu
docker compose -f docker-compose.webui-only.yml up -d
```

Откройте **http://localhost:3000** (или `http://IP_СЕРВЕРА:3000`). Модели из установленной Ollama появятся в интерфейсе автоматически.

**Остановка:** `docker compose -f docker-compose.webui-only.yml down`

---

## Продакшен

Создайте `.env`, при необходимости задайте `WEBUI_SECRET_KEY` (например: `openssl rand -hex 32`). Закройте лишние порты фаерволом и поставьте HTTPS (Nginx/Caddy) перед Open WebUI.

---

## Изменения

- **docker-compose.webui-only.yml** — вариант только с Open WebUI для подключения к Ollama на хосте (`host.docker.internal:11434`). Используйте, когда Ollama уже установлена на сервер и модели скачаны; образ Ollama в Docker не нужен.
