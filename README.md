[![Main Kittygram Workflow](https://github.com/AlekseyEMv/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/AlekseyEMv/kittygram_final/actions/workflows/main.yml)


# Kittygram - Социальная сеть для любителей котиков

## Описание проекта
Kittygram - это социальная сеть, где пользователи могут делиться фотографиями своих котиков, общаться и находить единомышленников. Проект развернут на том же сервере, что и приложение Taski, и доступен по отдельному доменному имени.

## Функциональность
* Загрузка и просмотр фотографий котиков
* Регистрация и аутентификация пользователей
* Личное пространство пользователя
* Система лайков и комментариев
* Панель администратора для управления контентом
* Интеграция с фронтендом
* Хранение медиафайлов

## Стек технологий
* **Backend**: Django REST Framework
* **Frontend**: React.js
* **База данных**: PostgreSQL
* **WSGI сервер**: Gunicorn
* **Веб-сервер**: Nginx
* **SSL/TLS**: Let's Encrypt
* **CI/CD**: GitHub Actions

## Развертывание проекта на сервере c Linux
1. Установка консольную утилиту curl, которая скачивать файлы по команде пользователя:
```bash
sudo apt update
sudo apt install curl
```

2. Скачивание скрипта для установки Docker с официального сайта:
```bash
curl -fSL https://get.docker.com -o get-docker.sh
```

3. Запуск сохранённого скрипта:
```bash
sudo sh ./get-docker.sh
```

4. Установка утилиты Docker Compose:
```bash
sudo apt install docker-compose-plugin
```

5. Копирование на сервер в директорию kittygram/ файл docker-compose.production.yml.

6. Настройка файла .env на сервер, в директорию kittygram/

7. Запуск проекта на сервере в режиме «демона» из директории, в которой размещён файл конфигурации docker-compose.production.yml:
```bash
sudo docker compose -f docker-compose.production.yml up -d
```

8. Выполните миграции базы данных:
```bash
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
```

9. Копирование статических файлов бэкенда:
```bash
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /backend_static/static/
```

10. Настройка Nginx:
```bash
sudo nano /etc/nginx/sites-enabled/default
```

11. Проверка конфигурации Nginx:
```bash
sudo nginx -t
```

5. Перезагрузка конфигурации Nginx:
```bash
sudo certbot --nginx -d your-domain.com
```

## Настройка .env файла
```
# Базовые настройки
SECRET_KEY=your-secret-key
DEBUG=False
# Настройки безопасности
ALLOWED_HOSTS=your-domain.com

# Настройки базы данных
# Константа IS_POSTGRESQL определяет тип используемой базы данных.
# Значение True указывает на использование PostgreSQL в качестве основной СУБД
# В других случаях будет использована sqlite.
IS_POSTGRESQL=True
DB_NAME=kittygram
DB_USER=kittygram_user
DB_PASSWORD=your-db-password
DB_HOST=localhost
DB_PORT=5432

```

## Структура проекта
```
kittygram_final
├── .env.example
├── .github
│   └── workflows
│       └── main.yml # Файл с воркфлоу, который вы добавите
├── .gitignore
├── README.md
├── backend
│   ├── .dockerignore
│   ├── Dockerfile # Докерфайл для бэкенда
│   ├── README.md
│   ├── cats
│   ├── kittygram_backend
│   ├── manage.py
│   └── requirements.txt
├── docker-compose.production.yml
├── docker-compose.yml
├── frontend
│   ├── .dockerignore
│   ├── .gitignore
│   ├── Dockerfile
│   ├── README.md
│   ├── package-lock.json
│   ├── package.json
│   ├── public
│   └── src
├── nginx
│   ├── Dockerfile
│   └── nginx.conf
└── tests.yml # Файл с данными для проверки
```

## Автор
* **Разработчик**: [AlekseyEMv]
* **GitHub**: [[Профиль GitHub](https://github.com/AlekseyEMv)]
* **Email**: [lelik.ne@mail.ru]

Для вопросов и предложений обращайтесь по указанным контактным данным.