
# Node-RED WhatsApp + Ollama Integration

## О проекте

Этот проект — готовое решение для Node-RED, позволяющее отправлять и получать сообщения WhatsApp, а также интегрировать локальный Ollama (GPT-OSS:20b) для генерации текстов. Все зависимости управляются через `package.json`, что обеспечивает простое развертывание и переносимость.

## Возможности

- Интеграция с WhatsApp через node-red-contrib-whatsapp-link
- Отправка/получение текстовых и мультимедийных сообщений
- Использование локального Ollama (GPT-OSS:20b) для генерации ответов
- Полная изоляция и контроль версий

## Предварительные требования

- Node.js (LTS)
- npm
- Git
- Запущенный Ollama с моделью gpt-oss:20b (`ollama run gpt-oss:20b`)

## Установка

```bash
git clone [URL вашего репозитория]
cd node-red-whatsapp
npm install
```

## Запуск

```bash
npm start
```

Node-RED будет доступен по адресу http://127.0.0.1:1880

## Использование

- Откройте редактор Node-RED: http://127.0.0.1:1880
- Для отправки сообщений WhatsApp используйте узел `chats-out`
- Для генерации текста через Ollama используйте функцию:

```javascript
msg.url = "http://localhost:11434/api/generate";
msg.method = "POST";
msg.payload = {
		"model": "gpt-oss:20b",
		"prompt": msg.payload,
		"stream": false
};
return msg;
```
и передайте результат в узел http request.

## Управление узлами

**Важно:**  
Устанавливайте и удаляйте узлы только через npm, а не через Manage Palette!

- Добавить узел:
	```bash
	npm install node-red-contrib-имя-узла
	```
- Удалить узел:
	```bash
	npm uninstall node-red-contrib-имя-узла
	```

## Структура проекта

```
.
├── .node-red/           # Данные пользователя Node-RED
├── node_modules/        # Зависимости
├── package.json         # Описания зависимостей и скриптов
├── settings.js          # Настройки Node-RED
├── flows.json           # Ваши потоки Node-RED
├── flows_cred.json      # Секреты (в .gitignore)
├── README.md            # Этот файл
```

## Конфигурация

- Основные настройки — в `settings.js`
- Порт, безопасность, глобальные переменные — настраиваются там же
- Для интеграции Ollama убедитесь, что сервер Ollama запущен и модель загружена

## Лицензия

MIT. См. файл LICENSE.
