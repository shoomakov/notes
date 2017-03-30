## Node.js


```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
sudo apt-get install -y build-essential
```

link: https://nodejs.org/en/download/package-manager/


## Nginx


```
apt-get install nginx
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
