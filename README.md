# BitrixDocker
BitrixDocker позволяет легко и просто запускать **Bitrix CMS** на **Docker**.

## Введение
BitrixDocker облегчает разработку на Битрикс предоставляя готовые сервисы PHP, NGINX, MySQL и многие другие.

### Начало работы
- Склонируйте репозиторий bitrixdocker
```
git clone https://github.com/ZxKill/bitrixDocker.git
```

- Выполните настройку окружения

Скопируйте файл `.env_template` в `.env`

```
cp -f .env_template .env
```
⚠️ Если у вас мак или windows, то удалите строчку /etc/localtime:/etc/localtime/:ro из docker-compose

По умолчнию используется nginx php7, эти настройки можно изменить в файле ```.env```. Также можно задать путь к каталогу с сайтом и параметры базы данных MySQL.


```
PHP_VERSION=php7           # Версия php 
WEB_SERVER_TYPE=nginx      # Веб-сервер nginx/apache
MYSQL_DATABASE=bitrix      # Имя базы данных
MYSQL_USER=bitrix          # Пользователь базы данных
MYSQL_PASSWORD=123         # Пароль для доступа к базе данных
MYSQL_ROOT_PASSWORD=123    # Пароль для пользователя root от базы данных
INTERFACE=0.0.0.0          # На данный интерфейс будут проксироваться порты
SITE_PATH=/var/www/bitrix  # Путь к директории Вашего сайта

```

- Запустите bitrixdock
```
docker-compose up -d
```
Чтобы проверить, что все сервисы запустились посмотрите список процессов ```docker ps```.  
