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
  4. Установка Portainer для удаленного управления контейнерами
  ```
    docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
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
2. Открыть терминал по адресу папки
3. Запуск docker-compose скрипта. Запускать из под пользователя без root и админских прав
```
  docker-compose up -d
```
4. Открыть файл seatable.service
    - User=$USER #указать пользователя от которого запускается сервис
5. Скопировать файл seatable.service в папку:
```
  /etc/systemd/system
```
команда с правами root
```
  cp seatable.service /etc/systemd/system
```
6. Добавить сервис в автозапуск #root права
```
  systemctl enable seatable.service
```
7. Создать суперпользователя
```
  docker exec -it seatable /shared/seatable/scripts/seatable.sh superuser
```

</p>
</details>
