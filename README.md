# CI/CD для многоконтейнерного веб-приложения
[![Django-app workflow](https://github.com/Viktoria-create/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)]

Цель проекта - практическое применение сервиса GitHub Actions для автоматизации 
процессов тестирования и развертывания многоконтейнерного веб-приложения на сервере.

## Стек технологий
- Python 3.7
- Django 2.2.16
- Django Filter 21.1
- Django REST Framework 3.12.4
- Simple JWT 5.2.0
- Postgresql 13.0
- Nginx 1.21.3
- Gunicorn 20.0.4

## Описание веб-приложения
Веб-приложение будет упаковано в три отдельных docker контейнера:
- web - контейнер с веб-приложением на фреймворке Django
- db - контейнер с базой данных postgresql
- nginx - контейнер с nginx сервером

**Веб-приложение**

Создано на фрэймворке Django. Работает в отдельном контейнере на WSGI сервере 
[Gunicorn](https://gunicorn.org/)

Более детальную информацию по функционалу приложения можно посмотреть [здесь](https://github.com/Viktoria-create/api_yamdb#readme)

Образ для развертывания docker контейнера с приложением хранится на [dockerhub](https://hub.docker.com/repository/docker/viktoriakosh/api_yamdb).

**База данных**

В проекте используется база данных [Postgresql](https://www.postgresql.org/).

Для запуска докер контейнера используется образ [postgres:13.0-alpine](https://hub.docker.com/_/postgres/tags?page=1&name=13.0-alpine)

**Nginx сервер**

Nginx сервер работает в отдельном контейнере, обеспечивая доступ к приложению,
а так же раздает статические файлы. В рамках данного проекта используется
незащищенный протокол [http](https://ru.wikipedia.org/wiki/HTTP). Для развертывания 
docker контейнера используется образ [nginx:1.21.3-alpine](https://hub.docker.com/_/nginx/tags?page=1&name=1.21.3-alpine)


## Описание CI/CD
CI/CD состоит из четырех этапов и автоматически запускается при push-операции в репозиторий GitHub:
1. Тестирование кода на соответствие PEP8 и функциональные тесты с pytest.
2. Создание образа веб-приложения и отправка его на dockerhub.
3. Развертывание многоконтейнерного веб-приложения на сервере.
4. Отправка сообщения в telegram об успешном завершении.


## Требования к удаленному серверу
На удаленном сервере должен быть настроен доступ по ssh, установлен docker и docker-compose.
Так же в домашнюю директорию пользователя, от имени которого будет организован доступ к серверу,
необходимо скопировать файл `docker-compose.yaml` из корневого каталога проекта, и файл конфигурации 
`infra/nginx/default.conf`, который необходимо разместить в `/home/<username>/nginx/default.conf`

## Поверка проекта 
 [WEB Django REST framework](http://158.160.1.217/api/v1/)

 **Более подробно по запросам смотрите в [Redoc](http://158.160.1.217/redoc)**
