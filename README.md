# PHP Link-Reformator (web application)

## Getting Started
This application requires you to hide real links by replacing it with fake, that will redirect you.

### Prerequisites
This application is simple, but to run it you need to have php local server and other requirements , so in my case I used [LEMP stack](https://www.digitalocean.com/community/tutorials/what-is-lemp):
* PHP 7.0+
* local web server (nginx in my case)
* PostgreSql Database

### Installing (ArchLinux)

1. Install nginx
```
$ sudo pacman -S nginx
$ sudo systemctl enable nginx
$ sudo systemctl start nginx
$ sudo systemctl status nginx
```
(to check if nginx works, go to http://localhost/)

2. Install PostgreSql 
```
$ sudo pacman -S postgresql
$ sudo -iu postgres
[postgres]$ initdb -D /var/lib/postgres/data
(next return to the regular user using exit)
Finally, start and enable the postgresql.service.
[postgres]$ createuser --interactive
$ createdb netgame

```

3) Install PHP & PHP-FPM
```
$ sudo pacman -S php php-fpm
$ sudo systemctl enable php-fpm
$ sudo systemctl start php-fpm
$ sudo systemctl status php-fpm (check if works)
-------------------------------------------------
$ sudo vim /etc/nginx/nginx.conf
add the changes: 
location / {
root   /usr/share/nginx/html;
index  index.html index.htm index.php;
}
location ~ \.php$ {
fastcgi_pass   unix:/var/run/php-fpm/php-fpm.sock;
fastcgi_index  index.php;
root   /usr/share/nginx/html;
include        fastcgi.conf;
}

(save the file and restart both Nginx and PHP-FPM for the changes to come into effect)
$ sudo systemctl restart nginx
$ sudo systemctl restart php-fpm
```

## Running the application

1) upload project folder and files to your system (better download zip archive)

2) create and save nginx config in 
```$ sudo nano /etc/nginx/sites-enabled/symfony```
(paste text from 'nginx_conf.txt', but change root to your)

3) import database 
```
$ psql -U [username] [dbname] < dbexport.pgsql
```
  change "DATABASE_URL=..." to your in '.env' and in 'webby/public/upload.php' cnahge variable 
```
DATABASE_URL="postgresql://[user]:[password]@127.0.0.1:5432/[database_name]?serverVersion=13&charset=utf8"
```

4) go to http://netgame.localhost/ and try to create new links 

## Note

To avoid some errors, you can install composer and its dependencies (https://symfony.com/doc/4.1/setup/composer.html).

## Built With

* [LEMP stack](https://www.linuxtechi.com/install-lemp-stack-on-arch-linux/) - a collection of open-source software
* [Symfony](https://symfony.com/) - a PHP framework for web projects
* [Bootstrap 4](https://getbootstrap.com/docs/4.0/getting-started/introduction/) - a framework for building responsive, mobile-first sites

## Author

**Daniel Popov** - *Junior PHP Developer* - [Lewis1727](https://github.com/Lewis1727)

