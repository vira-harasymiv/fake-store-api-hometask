# fake-store-api-hometask

## How to start

```bash
git init
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/vira-harasymiv/fake-store-api-hometask.git
git push -u origin main
```

Цей репозиторій містить колекцію Postman для практичних тестів API (файли в каталозі `tests/`) і приклади використання `newman` для запуску тестів з генерацією HTML-звіту через `newman-reporter-htmlextra`.

**Вміст репозиторію**

- `tests/` — Postman collection(и). Наприклад: `tests/fake-store-api.postman_collection.json`.
- `newman/` — збережені HTML-репорти від `newman`.
- `package.json` — (опціонально) залежності та скрипти, якщо додаються.

**Передумови**

- Встановлений Node.js та `npm`.

**Встановлення**

1. Глобальний варіант (швидкий):

```powershell
npm install -g newman newman-reporter-htmlextra
```

2. Локальний варіант (рекомendовано для CI або проєктів):

```powershell
npm install --save-dev newman newman-reporter-htmlextra
```

Після локальної інсталяції можна запускати через `npx newman ...`.

**Як запускати тести**

Запуск базовий (мінімальний):

```powershell
newman run tests/fake-store-api.postman_collection.json -r htmlextra
```

Якщо ви встановили пакети локально, використайте `npx`:

```powershell
npx newman run tests/fake-store-api.postman_collection.json -r htmlextra
```

Додаткові опції:

- Передати файл середовища Postman: `-e path/to/env.json`.
- Використати дані для ітерацій: `--iteration-data path/to/data.csv`.
- Згенерувати кілька репортерів: `-r htmlextra,cli`.

**Рекомендація для CI (npm-скрипт)**

Додайте в `package.json` (опціонально):

```json
"scripts": {
	"test:newman": "newman run tests/fake-store-api.postman_collection.json -r htmlextra --reporter-htmlextra-export newman/fake-store-api-report.html"
}
```

Тоді у CI або локально запустіть:

```powershell
npm run test:newman
```

**Де знайти звіт**
Після запуску звіт буде збережено у файлі `newman/fake-store-api-report.html`. Відкрийте його у браузері.

**Поради**

- Якщо директорія `newman/` не існує, `newman` створить файл, але краще перевірити права запису.
- Для відладкових виводів додайте репортер `cli`: `-r htmlextra,cli`.

Якщо хочете, можу додати `package.json`-скрипт прямо в репозиторій або приклади для CI (GitHub Actions, Azure Pipelines тощо).
