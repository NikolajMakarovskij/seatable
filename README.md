# Инструкция по развертыванию seatable в redos

## установка и настройка docker-compose 
<details><summary>Команды</summary>
<p>

  1. Установка docker-compose
  ```
    dnf install docker docker-compose
  ```  
  2. Добавление в автозапуск
  ```
    systemctl enable docker
  ```
  3. Запуск docker без root прав
  ```
    groupadd docker
  ```
  ```
    usermod -aG docker $USER
  ```

</p>
</details>

## Запуск seatable
<details><summary>Команды</summary>
<p>

1. Открыть файл .env 
   - MYSQL_ROOT_PASSWORD=  # Пароль для базы данных
   - MYSQL_LOG_CONSOLE=true
   - DB_HOST=db #оставить. db - имя сервиса с базой данных
   - DB_ROOT_PASSWD=  # Пароль для базы данных, должен совпадать с MYSQL_ROOT_PASSWORD
   - SEATABLE_SERVER_LETSENCRYPT=False # сертификат SSL, True при наличии сертификата и включения соединени HTTPS
   - SEATABLE_SERVER_HOSTNAME= #имя хоста
   - TIME_ZONE=Asia/Yekaterinburg #часовой пояс
2. Запуск docker-compose скрипта. Запускать из под пользователя без root и админских прав
```
  docker-compose up -d
```
3. Запуск seatable.
```
  docker exec -d seatable /shared/seatable/scripts/seatable.sh start
```
   - docker exec - обращение к контейнеру
   - docker exec имя_контейнера команда - синтаксис
4. Создать суперпользователя
```
  docker exec -it seatable /shared/seatable/scripts/seatable.sh superuser
```

</p>
</details>
