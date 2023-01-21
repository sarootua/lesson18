1. docker swarm init
docker info 2>&1 | grep  "Swarm:".* - Перепровіряємо активізувався swarm чи ні


2. створюэмо файл на хості з нашим секретом mysql_root_pass
echo "wordpress" > mysql_root_pass

наш секрет буде доступний в контейнері /run/secrets/mysql_root_pass після того як ми запустимо наш проект

в нашому проекті добавляємо блок
secrets:
  mysql_root_pass:
    file: ./mysql_root_pass

в описі нашого сервісу добавляємо блок
secrets:
- mysql_root_pass

та міняємо environment для MYSQL_ROOT_PASSWORD
MYSQL_ROOT_PASSWORD_FILE: /run/secrets/mysql_root_pass

Перепровіряємо:
 - docker compose up -d 
 - docker exec -it lesson18-db-1 cat /run/secrets/mysql_root_pass 

тут буде наш секрет

аналогічно робимо для других змінніх