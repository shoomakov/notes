## Node.js


```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install -y build-essential
```

link: https://nodejs.org/en/download/package-manager/


## Nginx


```
nano /etc/apt/sources.list
```
Добавляем строчки:
```
# jessie-backports official repo
deb http://ftp.ru.debian.org/debian/ jessie-backports main contrib non-free
deb-src http://ftp.ru.debian.org/debian/ jessie-backports main contrib non-free

# nginx official repo
deb http://nginx.org/packages/debian/ jessie nginx
deb-src http://nginx.org/packages/debian/ jessie nginx
```

Далее:
```
wget http://nginx.org/keys/nginx_signing.key
apt-key add nginx_signing.key
apt-get update && apt-get install nginx
```

Вероятно после обновления служба nginx в systemd будет замаскирована:
```
systemctl unmask nginx
systemctl restart nginx
```

Если нужно апгрейдить Nginx, то перед всеми этими действиями нужно:
```
apt-get remove nginx nginx-common
```


## Forever


```
npm install forever -g
```

## Бэкап конфигов


```
tar zcvf /root/etc.backup.tar.gz /etc/
```

## php-fpm 7


```
echo 'deb http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list
echo 'deb-src http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list
apt-get update
```
После скопировать NO_PUBKEY
```
gpg --keyserver keys.gnupg.net --recv-key <тут пабкей>
gpg -a --export <тут пабкей> | sudo apt-key add -
apt-get install php-fpm
```

Необходимо дать права Nginx'y, иначе велика вероятность, что получите ошибку:
```
nano /etc/php/7.0/fpm/pool.d/www.conf
```
Приводим следующие переменные к такому же виду (имя юзера nginx можно подсмотреть в ```/etc/nginx/nginx.conf```):
```
listen.owner = nginx
listen.group = nginx
listen.mode = 0666
```

Мастхэв модули:
```
apt-get install php-mysql php-curl php7.0-mbstring
```

Перезагрузка php-fpm:
```
systemctl restart php7.0-fpm
```

## MySQL 5.7

Качаем deb-пакет отсюда https://dev.mysql.com/downloads/file/?id=468400

```
wget https://dev.mysql.com/get/mysql-apt-config_0.8.3-1_all.deb
dpkg -i *.deb
apt-get update
apt-get install mysql-server
```
Если обновляете до версии 5.7, то еще:

```
mysql_upgrade -u root -p
service mysql restart
```
