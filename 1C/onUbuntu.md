# Xorg fonts
```apt-get install xfonts-100dpi```
```apt-get install xfonts-75dpi```
```apt-get install xfonts-cyrillic```

```apt-get install libx11-dev libxfixes-dev libssl-dev libpam0g-dev libtool libjpeg-dev flex bison gettext autoconf libxml-parser-perl libfuse-dev xsltproc libxrandr-dev python-libxml2 nasm xserver-xorg-dev fuse git```
```# git clone git://github.com/neutrinolabs/xorgxrdp```
```# git clone git://github.com/neutrinolabs/librfxcodec```
```# git submodule init```
```# git submodule update```
```# cd librfxcodec```
```# ./bootstrap```
```# ./configure```
```# make```
```# make install```
```# cd..```
```# cd xorgxrdp/```
```# ./bootstrap```
```# ./configure```
```# make```
```# make install```
```# cd ..```
```# ./bootstrap```
```# ./configure –enable-fuse –enable-rfxcodec –enable-fuse –enable-jpeg```
```# make```
```# make install```

Editar os arquivos:

```# nano /lib/systemd/system/xrdp.service```
[Unit]
Description=xrdp daemon
Requires=xrdp-sesman.service
After=syslog.target network.target xrdp-sesman.service
[Service]
Type=forking
PIDFile=/var/run/xrdp.pid
#EnvironmentFile=/etc/sysconfig/xrdp
ExecStart=/usr/local/sbin/xrdp $XRDP_OPTIONS
ExecStop=/usr/local/sbin/xrdp $XRDP_OPTIONS –kill
[Install]
WantedBy=multi-user.target
-> xrdp-sesman.service
```# nano /lib/systemd/system/xrdp-sesman.service```

[Unit]
Description=xrdp session manager
After=syslog.target network.target
StopWhenUnneeded=true
[Service]
Type=forking
PIDFile=/var/run/xrdp-sesman.pid
#EnvironmentFile=/etc/sysconfig/xrdp
ExecStart=/usr/local/sbin/xrdp-sesman $SESMAN_OPTIONS
ExecStop=/usr/local/sbin/xrdp-sesman $SESMAN_OPTIONS –kill
[Install]
WantedBy=multi-user.target

```# systemctl enable xrdp.service```
```# systemctl enable xrdp-sesman.service```
```# systemctl daemon-reload```

https://github.com/neutrinolabs/xrdp/wiki/Building-on-Debian-8
