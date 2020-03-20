# 4011 Repository Setup Guide

## Pre-Requirements

* Fresh install of Ubuntu in VirtualBox
* VirtualBox Guest Editons for screen scaling/bidirectional copying
* VScode
* git
    - sudo apt install git
* vim
    - sudo apt install vim
* Ports fed through to virtual
    - Devices - Segger JLink

## gcc-arm-none-eabi 
* How to Install arm-none-eabi-gcc for Linux
    - sudo add-apt-repository ppa:team-gcc-arm-embedded/ppa
    - sudo apt-get update
    - sudo apt-get install gcc-arm-embedded

* How to Install arm-none-eabi-gcc for OSX
    - brew tap ArmMbed/homebrew-formulae
    - brew install arm-none-eabi-gcc

## Installing Segger JLink
- download from https://www.segger.com/downloads/jlink/
- J-Link Software and Documentation pack for Linux, DEB installer, 64-bit
sudo dpkg -i ~/Downloads/jlink_5.2.7_x86_64.deb


## Requirements:
1. git installation
2. python 3.7
3. Linux/MAC OS
4. JLink Debugger/Programmer e.g. JLink EDU Mini
5. JLink Software and Drivers i.e. JLinkExe, JLinkRTT, etc
6. ARM GCC compiler - i.e. gcc-arm-none-eabi-8-2018-q4-major

## Generate SSH Key
- ssh-keygen -t rsa -C "example@example@uqconnect.edu.au"
- ssh-add
- then copy the key from id_rsa.pub to your github account

## Setup the Repository

1. git clone https://github.com/JordanYates/freertos_open.git
2. run the repo_setup.sh script

## Set up environment variables
### Linux
add the following lines to ~/.bashrc 

- export PATH=<repo path>/pacp-tools/tools:$PATH
- export PATH=<repo path>/pacp-tools/pyclasses:$PATH
- export PATH=<repo path>/pacp-freertos/tools:$PATH
- export PYTHONPATH=<repo path>/pacp-tools/pyclasses:$PYTHONPATH
- export PYTHONPATH=<repo path>/pacp-freertos/ pyclasses:$PYTHONPATH

run source ~/.bashrc

## Compile and flash an app:

### compiling the app unifiedbase:
    cd unifiedbase
    make TARGET=argon tdf - this needs to be done once
    make TARGET=argon debug - to compile

### flashing an app
connect your jlink EDU mini  
    make TARGET=argon flashdbg -j 

### tips:
    - make TARGET=argon help - generates help message
    - make TARGET=argon jlinksn - get serial numbers of devices connected - useful for multiple devices connected
    - make TARGET=argon JLINK=<serial number> - needed when multiple devices connected to computer or it will give you error, alternatively just take one out

## running the app: unifiedbase
to display any meaningful output we must run baselisten, an app that listens for incoming BLE packets 

    - cd pacp-tools
    - ./baselisten --serial /dev/ttyACM0

you can determine the serial device by typing 
    - ls /dev/tty*
which will display all the serial devices     




