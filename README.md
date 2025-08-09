# Auth Service (FastAPI + PostgreSQL + Docker)

Авторизация

## Стек
- Python 3.12, FastAPI
- SQLAlchemy 2.0
- PostgreSQL 15
- Docker / docker-compose
- JWT (python-jose), bcrypt (passlib)

## Быстрый старт

1) Скопируйте `.env.example` → `.env` и при необходимости измените значения.
   В контейнере БД используется хост `db`, БД `authdb`, пользователь/пароль `postgres/postgres`.

2) Запустите сервисы:
```bash
docker compose up --build
```

3) Откройте http://localhost:8000 — увидите демо-страницу с входом/регистрацией.

4) REST:
- POST `/api/register` `{ "email": "...", "password": "..." }`
- POST `/api/login` `{ "email": "...", "password": "..." }` → `{ "access_token": "...", "token_type": "bearer" }`

## Замечания по реализации

- Таблицы создаются на старте (для демо). В реальном проекте используйте Alembic.
- Валидация email на уровне API обеспечена через `EmailStr` (Pydantic).
- Пароли хэшируются через `passlib[bcrypt]`.
- Токены — JWT HS256, таймаут берётся из `.env`.
- Конфиги загружаются через `pydantic-settings`.

## Локальная разработка без Docker
Создайте и активируйте виртуальное окружение, установите зависимости:
```bash
pip install -r requirements.txt
uvicorn app.main:app --reload
```
Не забудьте настроить `DATABASE_URL` на локальный PostgreSQL и создать БД.

---
