# lxde

---

```
apt-get install lxde
reboot
```


# xrdp

---

```
apt-get install git autoconf libtool pkg-config gcc g++ make  libssl-dev libpam0g-dev libjpeg-dev libx11-dev libxfixes-dev libxrandr-dev  flex bison libxml2-dev intltool xsltproc xutils-dev python-libxml2 g++ xutils libfuse-dev libmp3lame-dev nasm libpixman-1-dev xserver-xorg-dev
git clone --recursive https://github.com/neutrinolabs/xrdp
cd xrdp
git clone git://github.com/neutrinolabs/xorgxrdp
./bootstrap
./configure
make
make install
cd librfxcodec
./bootstrap
./configure
make
make Install
cd ..
cd xorgxrdp/
./bootstrap
./configure
make
make install
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

#### Install fonts
```
apt-get install xfonts-100dpi xfonts-75dpi xfonts-cyrillic
```

# locale / keyboard

---

```
nano /etc/default/locale
```
```
LANG="ru_RU.UTF-8"
```
```
dpkg-reconfigure locales
```

Приводим ```/etc/xrdp/xrdp_keyboard.ini``` к виду:
```
[default]
; keyboard_type and keyboard_subtype is not read for default section. It
; is only a placeholder to keep consistency. Default model/variant are
; platform dependent, and could be overridden if needed.
keyboard_type=0
keyboard_subtype=0

; user could override variant and model, but generally they should be inferred
; automatically based on keyboard type and subtype
;variant=
;model=

; A list of supported RDP keyboard layouts
rdp_layouts=default_rdp_layouts
; The map from RDP keyboard layout to X11 keyboard layout
layouts_map=default_layouts_map

[default_rdp_layouts]
rdp_layout_us=0x00000409
rdp_layout_de=0x00000407
rdp_layout_fr=0x0000040C
rdp_layout_it=0x00000410
rdp_layout_jp=0x00000411
rdp_layout_jp=0xe0010411
rdp_layout_jp=0xe0200411
rdp_layout_jp=0xe0210411
rdp_layout_kr=0x00000412
rdp_layout_ru=0x00000419
rdp_layout_se=0x0000041D
rdp_layout_ch=0x00000807
rdp_layout_pt=0x00000816
rdp_layout_br=0x00000416
rdp_layout_pl=0x00000415

; <rdp layout name> = <X11 keyboard layout value>
[default_layouts_map]
rdp_layout_us=us
rdp_layout_de=de
rdp_layout_fr=fr
rdp_layout_it=it
rdp_layout_jp=jp
rdp_layout_kr=kr
rdp_layout_ru=ru
rdp_layout_se=se
rdp_layout_ch=ch
rdp_layout_pt=pt
rdp_layout_br=br(abnt2)
rdp_layout_pl=pl

[rdp_keyboard_ru]
keyboard_type=4
keyboard_subtype=1
model=pc105
options=grp:alt_shift_toggle
rdp_layouts=default_rdp_layouts
layouts_map=layouts_map_ru

[layouts_map_ru]
rdp_layout_us=us,ru
rdp_layout_ru=us,ru
```
В скрипт ```/etc/xrdp/startwm.sh``` после Xsession добавляем следующее:
```
setxkbmap -layout "ru,us" -model "pc105" -option "grp:alt_shift_toggle,grp_led:scroll"
```
Также в самом GUI поставить галочку в "настройках раскладки клавиатуры" - **не сбрасывать существующие настройки**

# Timezone и синхронизация времени

---
```
dpkg-reconfigure tzdata
apt-get install ntp
service ntp stop
ntpdate -s time.nist.gov
service ntp start
```

# 1C, Libreoffice и др.

---
```
apt-get install libreoffice
apt-get install libreoffice-l10n-ru
```
Распаковываем файлы **deb64.tar.gz** и **client.deb64.tar.gz** из дистрибутива 1С 8.3 в одну папку, затем:
```
dpkg -i 1c*.deb
apt-get -f install
apt-get install ttf-mscorefonts-installer
apt-get install imagemagick
```

Настроить пользователей...
