# Сайт для инди-команды разработчиков

Современный веб-сайт для инди-команды разработчиков игр, вдохновленный дизайном сайта игры Marathon. Сайт включает в себя админ-панель для управления контентом и систему подачи заявок на вступление в команду.

## Содержание

- [Особенности](#особенности)
- [Технологии](#технологии)
- [Установка и запуск](#установка-и-запуск)
- [Структура проекта](#структура-проекта)
- [Безопасность](#безопасность)
- [Администрирование](#администрирование)
- [API Endpoints](#api-endpoints)
- [Лицензия](#лицензия)

## Особенности

- Современный адаптивный дизайн, вдохновленный сайтом игры Marathon
- Полноценная админ-панель для управления контентом сайта
- Возможность редактирования текстов и изображений без изменения кода
- Система подачи и управления заявками на вступление в команду
- Аутентификация и авторизация с разделением прав доступа
- Защита от основных типов атак (XSS, CSRF, инъекции и т.д.)
- Полностью адаптивный дизайн для мобильных устройств

## Технологии

### Backend
- Node.js
- Express.js
- MongoDB (Mongoose)
- JWT для аутентификации
- Multer для загрузки файлов
- Sanitize-HTML для защиты от XSS
- Helmet для HTTP-заголовков безопасности
- Express-rate-limit для защиты от DDoS

### Frontend
- React.js
- Redux Toolkit для управления состоянием
- React Router для маршрутизации
- Styled Components для стилизации
- React Icons для иконок
- React Toastify для уведомлений
- Axios для HTTP-запросов

## Установка и запуск

### Предварительные требования
- Node.js (v14+)
- MongoDB (локально или удаленно)
- npm или yarn

### Шаги установки

1. Клонируйте репозиторий:
```bash
git clone https://github.com/HologramAlice/Project_Apollo.git
cd Project_Apollo
```

2. Установите зависимости:
```bash
npm install-all
```

3. Создайте файл `.env` в корневой директории проекта и добавьте следующие переменные:
```
NODE_ENV=development
PORT=5000
MONGO_URI=mongodb://localhost:27017/indie-dev-team
JWT_SECRET=your_jwt_secret_key_here
JWT_EXPIRE=30d
UPLOAD_PATH=./uploads
ADMIN_SECRET_KEY=your_admin_secret_key_here
```

4. Запустите сервер и клиент в режиме разработки:
```bash
npm run dev
```

5. Создайте первого администратора, отправив POST-запрос на `/api/auth/create-admin` с данными:
```json
{
  "name": "Admin",
  "email": "admin@example.com",
  "password": "your_password",
  "secretKey": "your_admin_secret_key_here"
}
```

## Структура проекта

```
indie-dev-team-site/
├── client/                 # Frontend (React)
│   ├── public/             # Статические файлы
│   └── src/                # Исходный код React
│       ├── components/     # React компоненты
│       ├── pages/          # Страницы приложения
│       ├── redux/          # Redux store и slices
│       └── assets/         # Изображения и другие ресурсы
├── config/                 # Конфигурация сервера
├── controllers/            # Контроллеры API
├── middleware/             # Middleware функции
├── models/                 # Mongoose модели
├── routes/                 # API маршруты
├── uploads/                # Загруженные файлы
├── .env                    # Переменные окружения
├── package.json            # Зависимости и скрипты
└── server.js               # Точка входа сервера
```

## Безопасность

Проект включает в себя следующие меры безопасности:

- **JWT аутентификация**: Безопасная аутентификация с использованием JSON Web Tokens
- **Защита от XSS**: Санитизация HTML-контента с помощью sanitize-html
- **HTTP-заголовки безопасности**: Настройка заголовков с помощью Helmet
- **Ограничение запросов**: Защита от DDoS с помощью express-rate-limit
- **Валидация данных**: Проверка входных данных с помощью express-validator
- **Безопасное хранение паролей**: Хеширование паролей с помощью bcrypt
- **CORS**: Настройка Cross-Origin Resource Sharing

## Администрирование

### Создание администратора

При первом запуске необходимо создать администратора, отправив POST-запрос на `/api/auth/create-admin` с данными:

```json
{
  "name": "Admin",
  "email": "admin@example.com",
  "password": "your_password",
  "secretKey": "your_admin_secret_key_here"
}
```

Значение `secretKey` должно совпадать с `ADMIN_SECRET_KEY` в файле `.env`.

### Доступ к админ-панели

1. Войдите в систему, используя email и пароль администратора
2. После успешного входа вы будете перенаправлены на страницу админ-панели
3. В админ-панели вы можете:
   - Управлять контентом сайта (тексты, изображения)
   - Просматривать и обрабатывать заявки на вступление в команду

## API Endpoints

### Аутентификация

- `POST /api/auth/register` - Регистрация нового пользователя
- `POST /api/auth/login` - Вход в систему
- `GET /api/auth/profile` - Получение профиля пользователя
- `PUT /api/auth/profile` - Обновление профиля пользователя
- `POST /api/auth/create-admin` - Создание администратора (только при первом запуске)

### Контент

- `GET /api/content` - Получение всего контента
- `GET /api/content/:section` - Получение контента по секции
- `POST /api/content` - Создание нового контента (только для админа)
- `PUT /api/content/:id` - Обновление контента (только для админа)
- `DELETE /api/content/:id` - Удаление контента (только для админа)
- `POST /api/content/upload` - Загрузка изображения (только для админа)

### Заявки

- `POST /api/applications` - Создание новой заявки
- `GET /api/applications` - Получение всех заявок (только для админа)
- `GET /api/applications/:id` - Получение заявки по ID (только для админа)
- `PUT /api/applications/:id` - Обновление статуса заявки (только для админа)
- `DELETE /api/applications/:id` - Удаление заявки (только для админа)

## Лицензия

Этот проект распространяется под лицензией MIT. См. файл `LICENSE` для получения дополнительной информации.
