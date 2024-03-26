# kittygram_final
## Описание
  Данный сервис предоставляет Вам возможность делиться своими _котиками_ с сообществом __kittygram__.
  Вы можете добавить цвет котика, год рождения, фотографию и его достижения; отредактировать профиль котика.
  Чтобы использовать сервис, необходимо зарегестрироваться (```https://kittys.hopto.org/```).

Сервис предназначен только для котиков, размещение на нем собачек __запрещено__!

## Как запустить проект:
1. На ```https://github.com/``` сделайте форк и клонируйте репозиторий:
   ```https://github.com/PracticName/kittygram_final```
2. Заполните следующие переменные в файле .env (файл создайте в корне проекта)
   Пример:
   POSTGRES_DB=django 
   POSTGRES_USER=django
   POSTGRES_PASSWORD=password
   DB_NAME=kitty
   DB_HOST=db
   DB_PORT=5432
   SECRET_KEY=django
   ALLOWED_HOSTS=127.0.0.1,localhost,<ip сервера>,<твой домен>
   DEBUG=True
3. Запустите Docker
4. Запустите файл docker-compose.yml в корне проекта
   ```docker compose --build up```
   произойдет сборка образов и запуск контейнеров
5. Выполняем миграции и создайте пользователя
   ```docker compose exec backend pyhon manage.py migrate```
   ```docker compose exec backend pyhon manage.py createsuperuser```
6. Соберите статику
   ```docker compose exec backend pyhon manage.py collectstatic```
   ```docker compose exec backend backend cp -r /app/collected_static/. /backend_static/static```

Для деплоя на сервер на ```https://github.com/``` в репозитории проекта перейдите _Settings-->Secrets and variables-->Actions_.
Создайте следующие секреты через кнопку _New repository secret_
DOCKER_PASSWORD - пароль Docker
DOCKER_USERNAME - имя пользователя Docker
HOST - ip сервера
SSH_KEY - закрытый ключ для подключения к серверу
SSH_PASSPHRASE - пароль к закрытому кдючу
TELEGRAM_TO - ваш id telegram
TELEGRAM_TOKEN - ключ вашего бота в telegram
USER - имя пользователя на сервере

## Технологии
1. Полный список библиотек по фронтенду /frontend/package.json
2. Полный список библиотек по бекенду /backend/requirements.txt
3. Docker ```https://www.docker.com/```
4. Nginx ```https://nginx.org/```
5. Telegram ```https://telegram.org/```

## Примеры использования Api
- Список пользователей
  GET ```api/users/``` 
  **Ответ**
  ```
  {
    "count": 0,
    "next": "http://example.com",
    "previous": "http://example.com",
    "results": [
      {
        "email": "user@example.com",
        "id": 0,
        "username": "string"
      }
    ] 
  }
  ```

- Создание пользователя
  POST ```api/users/```
  ```
  {
    "email": "user@example.com",
    "username": "string",
    "password": "string"
  }
  ```
  **Ответ**
  ```
  {
    "email": "user@example.com",
    "username": "string",
    "id": 0,
    "password": "string"
  }
  ```
- Залогиниться
  POST ```api/token/login/```
  ```
  {
    "username": "string",
    "password": "string"
  }
  ```
  **Ответ**
  ```
  {
    "password": "string",
    "username": "string"
  }
  ```
- Разлогиниться
  ```api/token/logout/```  
  - Список достижений котиков
  GET ```api/achievements/```
  **Ответ**
  ```  
  [
    {
      "id": 0,
      "achievement_name": "string"
    }
  ]
  ```
- Создание достижений котика
  POST ```api/achievements/```  
  ```  
  {
    "achievement_name": "string"
  }
  ```
  **Ответ**
  {
    "id": 0,
    "achievement_name": "string"
  }
- Создание достижений котика
  GET ```api/achievements/{id}/``` 
  **Ответ**
  {
    "id": 0,
    "achievement_name": "string"
  }
- Создание котика
  POST ```api/cats/```  
  ```  
  {
    "name": "string",
    "color": "string",
    "birth_year": -9223372036854776000,
    "achievements": [
      {
        "achievement_name": "string"
      }
    ]
  }
  ```
  **Ответ**
  ```
  {
    "id": 0,
    "name": "string",
    "color": "string",
    "birth_year": -9223372036854776000,
    "achievements": [
      {
        "id": 0,
        "achievement_name": "string"
      }
    ],
    "owner": 0,
    "age": "string",
    "image": "http://example.com"
  }
  ```
- Получение котика
  GET ```api/cats/{id}```    
  **Ответ**
  ```
  {
    "id": 0,
    "name": "string",
    "color": "string",
    "birth_year": -9223372036854776000,
    "achievements": [
      {
        "id": 0,
        "achievement_name": "string"
      }
    ],
    "owner": 0,
    "age": "string",
    "image": "http://example.com"
  }
  ```

## Автор
  Агеев Алексей
