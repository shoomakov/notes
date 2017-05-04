## Musthave
```
apt-get install sudo curl git
```

## ZSH
```
sudo apt-get install zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
nano ~/.zshrc
```
Меняем строчку:
```
ZSH_THEME="bira"
```


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
Тут вставляем имя пользователя, от имени которого деплоится проект:
```
user = shoomakov
group = shoomakov
```

Мастхэв модули:
```
apt-get install php-mysql php-curl php7.0-mbstring php-cli php-xml
```

Перезагрузка php-fpm:
```
systemctl restart php7.0-fpm
```
## php5.6-fpm
**для некоторых древних проектов нужно и такое**

```
apt-get install software-properties-common
sudo LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install php5.6-fpm
sudo apt-get install php5.6-mysql
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

## Composer
Ключ тут: https://composer.github.io/pubkeys.html
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

## Node.js


```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install -y build-essential
```

link: https://nodejs.org/en/download/package-manager/


## Forever

```
npm install forever -g
```
