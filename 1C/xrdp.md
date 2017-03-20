#xrdp

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
