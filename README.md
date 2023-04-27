# Servidor-WEB-NGINX-PHP-PostgreSQL-phpPgAdmin-Letsencrypt-no-Debian-11

Vamos Instalar o NGINX

     apt install nginx
Vamos remover a assinatura do NGINX

     sed -i 's/# server_tokens/server_tokens/' /etc/nginx/nginx.conf
Vamos restartar o serviço

     systemctl restart nginx
Agora vamos instalar o PostgreSQL

     apt install postgresql postgresql-contrib
Torne-se o usuário Postgres

     su - postgres
Entre no terminal do banco

     psql
Defina a senha do seu banco e vamos instalar o adminpack

     \password postgres
     #Digite nova senha para postgres: 
     #Digite-a novamente:
     CREATE EXTENSION adminpack;
     \q 
     exit
