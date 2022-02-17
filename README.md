# wordpress
Foi cirado uma aplicação (site e banco de dados) utilizando o  Docker Compose, onde vamos criar e executar o container da aplicação e criar e executar o container com o banco de dados da aplicação como mostra abaixo: 

version: "3.7"
    
services:
  db_sql:
    restart: always
    image: mysql:${SQL_TAG}
    volumes:
      - sql_vol:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: ${DATABASE_ROOT_PASSWORD}
      MYSQL_DATABASE: ${DATABASE_DB_NAME}
      MYSQL_USER: ${DATABASE_USER}
      MYSQL_PASSWORD: ${DATABASE_PASSWORD}
    
  wordpress:
    restart: always
    depends_on:
      - db_sql
    image: wordpress
    volumes:
      - wordpress_vol:/var/www/html
    ports:
      - "8000:80"
    environment:
      WORDPRESS_DB_HOST: db_sql
      WORDPRESS_DB_USER: ${DATABASE_USER}
      WORDPRESS_DB_PASSWORD: ${DATABASE_PASSWORD}
      WORDPRESS_DB_NAME: ${DATABASE_DB_NAME}
volumes:
  sql_vol: {}
  wordpress_vol: {}
  
  
  # Foi criado um arquivo .env para proteger os dados sensiveis e versionalizar as imagens sem mexer no arquivo do compose. 
  
  
  O comando para rodar a aplicação é o:
  # docker-compose up -d 
  
  Para acessar a aplicação, será usado a URL:
  http://localhost:8080
  
