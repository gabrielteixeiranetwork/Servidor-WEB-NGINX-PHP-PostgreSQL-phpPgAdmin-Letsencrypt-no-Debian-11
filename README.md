# Servidor-WEB-NGINX-PHP-PostgreSQL-no-Debian-11

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
Vamos ajustar o arquivo vim /etc/postgresql/13/main/pg_hba.conf para conseguirmos validar a senha que acabamos de definir
![image](https://user-images.githubusercontent.com/94009104/234939842-138aa098-55f1-4aad-8257-e742448eb56c.png)
Vamos restartar o banco
     
     systemctl restart postgresql
Vamos instalar o PHP 7.4

     apt install php php-{fpm,cli,mysql,pear,gd,gmp,bcmath,mbstring,curl,xml,zip,json,pgsql}
Vamos fazer a integração do PHP com NGINX

     mv /etc/nginx/sites-available/default /etc/nginx/sites-available/default.original
Crie um novo 
     
     vim /etc/nginx/sites-available/default
Ajuste:
     
     server {
          listen 80;
          listen [::]:80;
 
          root /var/www/html;
          index index.php index.html index.htm;
 
          server_name _;
 
          location / {
              try_files $uri $uri/ =404;
          }
 
          location ~ \.php$ {
             include snippets/fastcgi-php.conf;
              fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
          }
     }
Teste a configuração

     nginx -t
Reinicie o NGINX e o PHP
     
     systemctl restart nginx php7.4-fpm
