Для запуска jira в контейнерe на хост-машине должен быть установлен docker и docker-compose.
Далее cоздаем каталоги в хост-системе для хранения данных jira + mysql и выставляем на них права:
   
```
     sudo mkdir -p /srv/jira
     sudo chmod 777 /srv/jira 
     sudo mkdir -p /srv/mysql
     sudo chmod 777 /srv/mysql 
``` 

Для работы jira будет созданы пустая БД jiradb и пользователь jirauser. При старте контейнера mysql  БД будет создана автоматически (расскомментированные строки в секции environment файла docker-compose.yml)
Запуск установки:
   
```
     docker-compose up -d
```

Открываем в браузере jira.office.lc и следуем инструкциям мастера установки. 
Подключение к мускулу по ip сервера
логин и пароль из конфига
```
      - MYSQL_USER=jirauser
      - MYSQL_PASSWORD=jirapasswd
```
сначала требуется ввести лицензионный ключ и только потом можно восстанавливаться из бекапа. На этом этапе можно ввести любую (evaluation, 30 дней) лицензию, в дальнейшем она заменится на "нужную".

При восстановлении jira из резервной копии подтягиваются только данные БД - attachments, avatars, logos нужно переносить вручную. После переноса выполняем:

```
     docker-compose restart jira
```

