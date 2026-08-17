# Marketplace Cards (форк UPAK)

Генератор карточек товаров для Wildberries и Ozon: селлер заполняет бриф → YandexGPT генерирует продающее описание, характеристики, преимущества → экспорт для маркетплейса.

Форк проекта [upak.space](https://upak.space) (репозитории Yuriuser1: Upak-frontend-NEW-v3 + UPAK-backend). Секреты удалены, структура сведена в один проект.

## Структура

- `app/`, `components/`, `lib/`, `hooks/` — фронтенд (Next.js 14, TypeScript, Tailwind, Framer Motion, Radix UI, Prisma)
- `server/` — бэкенд (FastAPI, один файл `main.py`):
  - `POST /create_payment` — создание платежа ЮKassa
  - `POST /yookassa-webhook` — вебхук оплаты
  - `POST /order` — генерация карточки через YandexGPT (yandexgpt-lite)
  - `POST /payment-confirm` — подтверждение оплаты
- `prisma/` — схема БД

## Запуск

### Бэкенд

```bash
cd server
pip install -r requirements.txt
cp .env.example .env   # заполнить ключи
uvicorn main:app --port 8000
```

### Фронтенд

```bash
npm install
npm run dev
```

## Нужные ключи

| Переменная | Где взять |
|---|---|
| `YANDEX_CHECKOUT_SHOP_ID` / `YANDEX_CHECKOUT_KEY` | Личный кабинет ЮKassa (сначала тестовый shopId 54401) |
| `YANDEX_GPT_API_KEY`, `YANDEX_GPT_FOLDER_ID` | Yandex Cloud → Foundation Models |
| `TELEGRAM_TOKEN` | @BotFather |

## Тарифы оригинала (для ориентира)

- Start — 349 ₽ / карточка
- Pro — 2 490 ₽ / 10 карточек

## Важно

- Оригинал без лицензии (all rights reserved) — для продакшна дописывать своё
- Все секреты оригинального автора удалены из этого форка
