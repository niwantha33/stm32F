
Subdirectory  -Install

git clone https://github.com/ve3wwg/stm32f103c8t6.git
cd ~/stm32f103f8t6
git clone https://github.com/libopencm3/libopencm3.git

#FreeRTOS
Go to http://www.freertos.org. download the latest official release from
SourceForge.

#Install FreeRTOS
cd ~/stm32f103c8t6/rtos
unzip ~/Downloads/FreeRTOSv10.0.1.zip

>> All the files will be here 
~/stm32f103c8t62/rtos/FreeRTOSv10.0.1
>> ~/stm32f103c8t6/rtos/Project.mk
>>gedit Project.mk 
change the V10.x.x
FREERTOS        ?= FreeRTOSv10.0.1
to latest version 
FREERTOS        ?= FreeRTOSv11.0.0

#ARM Cross Compiler 
1. Go to the site https://developer.arm.com.
2. Click on the link “Linux/Open Source.”
3. Scroll down and click on “ARM GNU Embedded Toolchain.”
4. Scroll down and click on the big button labeled “Downloads.”

sudo -i
cd /opt
tar xjf ~myuserid/Downloads/gcc-arm-none-eabi-6-2017-q2-
update-mac.tar.bz2

mv gcc-arm-none-eabi-6-2017-q2-update gcc-arm 

>>bin directory to your PATH:
export PATH="/opt/gcc-arm/bin:$PATH"

#Finally 
arm-none-eabi-gcc --version
type gcc

change the toolchain prefix, then the top-level ~/stm32f103c8t6/
Makefile.incl should be edited:
cd ~/stm32f103c8t6
gedit Makefile.incl

Modify the following line to suit and resave it:
PREFIX          ?= arm-none-eabi

>> type arm-none-eabi-gcc

#Build the Software
cd ~/stm32f103c8t6
make
#ST-Link V2 programmer

##Software Setup
cd ~
git clone https://github.com/texane/stlink.git
cd ./stlink
make
cd build/Release
sudo make install

sudo tar -xvf stlink_udev_rule.tar.bz2 -C /etc/udev/rules.d

sudo ldconfig
