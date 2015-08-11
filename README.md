Prerequisites:
* Ubuntu 15.04
* STM32F4 Discovery Board

Install software dependencies:
* sudo apt-get install build-essential git binutils-arm-none-eabi gcc-arm-none-eabi libnewlib-arm-none-eabi symlinks expect autoconf libusb-1.0 git libtool
'''
cd ~
mkdir .installed
cd .installed
wget -O openocd.tar.gz http://downloads.sourceforge.net/project/openocd/openocd/0.9.0/openocd-0.9.0.tar.gz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fopenocd%2Ffiles%2Fopenocd%2F0.9.0%2F&ts=1433259295&use_mirror=softlayer-dal
tar -zxf ./openocd.tar.gz
cd openocd-0.9.0
./configure --prefix=/usr --enable-stlink
make
sudo make install
'''

Update udev rules
'''
echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="0483", ATTR{idProduct}=="3748", MODE="0666", OWNER="'$USER'"' | sudo tee -a /etc/udev/rules.d/45-usb-stlink-v2.rules
sudo service udev restart
'''

Build:
* make clean && make release # OR
* make clean && make release-memopt # OR
* make clean && make debug

Deploy:
* make deploy

More info:
* [Template Project with Generic Makefile](http://istarc.wordpress.com/2014/07/01/stm32f4/)
* [In-circuit Debugging](http://istarc.wordpress.com/2014/07/06/stm32f4-in-circuit-debugging/)
