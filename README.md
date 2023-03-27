# wp-nginx
https://www.linuxcapable.com/how-to-install-wordpress-with-nginx-mariadb-php-on-ubuntu-linux/

sudo apt install nginx mysql-server mysql-client
sudo systemctl start nginx
sudo systemctl start mysql

sudo systemctl status nginx
sudo systemctl status mysql


sudo systemctl enable nginx
sudo systemctl enable mysql

78L4ds%J


GRANT ALL PRIVILEGES ON wpdb.* TO wpuser@localhost;

FLUSH PRIVILEGES;

sudo apt install php php-fpm php-mbstring php-bcmath php-xml php-mysql php-common php-gd php-cli php-curl php-zip php-imagick php-ldap php-intl

systemctl status php7.4-fpm.service



```nginx
server {
  listen 80;
  listen [::]:80;
  server_name www.example.com example.com;
  root /var/www/html/wordpress;
  index index.php index.html index.htm index.nginx-debian.html;

  location / {
    try_files $uri $uri/ /index.php?$args;
  }

  location ~* /wp-sitemap.*\.xml {
    try_files $uri $uri/ /index.php$is_args$args;
  }

  client_max_body_size 100M;

  location ~ \.php$ {
    fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
    include snippets/fastcgi-php.conf;
    fastcgi_buffer_size 128k;
    fastcgi_buffers 4 128k;
    fastcgi_intercept_errors on;
  }

  gzip on;
  gzip_comp_level 6;
  gzip_min_length 1000;
  gzip_proxied any;
  gzip_disable "msie6";
  gzip_types application/atom+xml application/geo+json application/javascript application/x-javascript application/json application/ld+json application/manifest+json application/rdf+xml application/rss+xml application/xhtml+xml application/xml font/eot font/otf font/ttf image/svg+xml text/css text/javascript text/plain text/xml;

  location ~* \.(?:css(\.map)?|js(\.map)?|jpe?g|png|gif|ico|cur|heic|webp|tiff?|mp3|m4a|aac|ogg|midi?|wav|mp4|mov|webm|mpe?g|avi|ogv|flv|wmv)$ {
    expires 90d;
    access_log off;
  }

  location ~* \.(?:svgz?|ttf|ttc|otf|eot|woff2?)$ {
    add_header Access-Control-Allow-Origin "*";
    expires 90d;
    access_log off;
  }

  location ~ /\.ht {
    access_log off;
    log_not_found off;
    deny all;
  }
}
```
mysqldump -u username -p dbname > dbexport.sql

mysqldump -uroot -p root YourDatabaseName > WantedSQLFile.sql



Type the following command to import sql data file:

$ mysql -u username -p -h localhost DATA-BASE-NAME < data.sql
In this example, import 'data.sql' file into 'blog' database using vivek as username:

$ mysql -u vivek -p -h localhost blog < data.sql
If you have a dedicated database server, replace localhost hostname with with actual server name or IP address as follows:

$ mysql -u username -p -h 202.54.1.10 databasename < data.sql
To export a database, use the following:

mysqldump -u username -p databasename > filename.sql
Note the < and > symbols in each case.
