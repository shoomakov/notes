# xrdp

---

```
sudo apt-get install git autoconf libtool pkg-config gcc g++ make  libssl-dev libpam0g-dev libjpeg-dev libx11-dev libxfixes-dev libxrandr-dev  flex bison libxml2-dev intltool xsltproc xutils-dev python-libxml2 g++ xutils libfuse-dev libmp3lame-dev nasm libpixman-1-dev xserver-xorg-dev
git clone --recursive https://github.com/neutrinolabs/xrdp
cd xrdp
git clone git://github.com/neutrinolabs/xorgxrdp
./bootstrap
./configure
make
sudo make install
cd librfxcodec
./bootstrap
./configure
make
sudo make Install
cd ..
cd xorgxrdp/
./bootstrap
./configure
make
sudo make install
cd ..
./bootstrap
./configure –enable-fuse –enable-rfxcodec –enable-fuse –enable-jpeg
```

#### Config xrdp.service
```
nano /lib/systemd/system/xrdp.service
```
```
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
```

#### Config sessman-service
```
nano /lib/systemd/system/xrdp-sesman.service
```
```
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
```

#### Enable xrdp
```
systemctl enable xrdp.service
systemctl enable xrdp-sesman.service
systemctl daemon-reload
```
