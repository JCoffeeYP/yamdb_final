![YaMDb-api workflow](https://github.com/JCoffeeYP/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
# Проект YaMDb

### Сервис YaMDb предназначен для сбора отзывов на различные произведения. Каждое произведение относится к той или иной категории ("Книги", "Фильмы", и т.д.). Пользователи могут оставлять текстовые отзывы и выставлять оценку от 0 до 10. На основе осреднённой оценки формируется рейтинг произведения. 

### В рамках данной работы реализовано API YaMDb

## Ресурсы API YaMDb

Resource | Description
:-------:|:-------:
auth     |аунтентификация
users    |пользователи
titles   |произведения
genres   |жанры произведений
reviews  |отзывы на произведения
comments |комментарии к отзывам

## Техническое описание

Technology    | Version
:-----------: | :-----------:
docker-compose| 3.8
Python        | 3.8.5
Nginx         | 1.19.3
PostgeSQL     | 12.4

## Инструкция по установке

1. При необходимости установить Docker и Docker-Compose ([руководство по установке](https://www.docker.com/get-started/ "https://www.docker.com/get-started"))
2. Склонировать проект 
3. Настроить базу данных PostgreSQL. Для этого необходимо в корне проекта создать файл `.env` и объявить следующие переменные:
- `DB_NAME=postgres`
- `DB_ENGINE=django.db.backends.postgresql`
- `POSTGRES_USER=postgres`
- `POSTGRES_PASSWORD=postgres` (При необходимости установить свой пароль)
- `DB_HOST=db`
- `DB_PORT=5432`
- `SECRET_KEY='cHaNgE-Me_NOW!!!'` (ОБЯЗАТЕЛЬНО СОЗДАТЬ СВОЙ ПАРОЛЬ ([Генератор secret key для Django-проектов](https://djecrety.ir/ "https://djecrety.ir/")))
- `HOSTS_LIST='web', 'localhost'` (Установить рабочий ip-адрес или указать доменное имя. Несколько адресов указываются через запятую)
4. Настроить nginx. Для этого в файле `./nginx/default.conf` указать используемый ip-адрес
5. В терминале развернуть контейнер командой `docker-compose up --build`
6. Создать новое окно терминала и выполнить следующие команды:
- `docker-compose exec web python manage.py migrate auth`
- `docker-compose exec web python manage.py migrate --run-syncdb`
- `docker-compose exec web python manage.py collectstatic --no-input`
7. Для создания суперпользователя воспользоваться командой `docker-compose exec web python manage.py createsuperuser`
8. Для заполения базы данных тестовыми объектами использовать команду `docker-compose exec web python manage.py loaddata fixtures.json`
9. Проект готов к работе!

## Эндпоинты

Все эндпоинты описаны по адресу http://84.201.141.255/redoc/

## Разработчик

Isaev Nikita