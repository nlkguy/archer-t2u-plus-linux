# TP-Link Archer T2U Plus a.k.a AC600 High-Gain


&nbsp;
[![Stargazers repo roster for @nlkguy/archer-t2u-plus-linux](https://reporoster.com/stars/nlkguy/archer-t2u-plus-linux)](https://github.com/nlkguy/archer-t2u-plus-linux/stargazers)
&nbsp;

## [Important] this repo is under scrutiny as the driver is not working properly , meantime [this](https://github.com/morrownr/8821au-20210708) is working , this repo will be updated shortly

## Table of contents

<p align = "left">
<a href="https://github.com/Krishak15/archer-t2u-plus-linux/edit/main/README.md#driver-for-debian-based-linux-distros-ubuntukali-linuxx86_64"> 1) Driver for Debian Based Linux Distros (Ubuntu/Kali Linux)(x86_64 </a> <br>
  <a href="https://github.com/Krishak15/archer-t2u-plus-linux/edit/main/README.md#driver-for-raspberry-pi-raspbian-os--kaliarm"> 2) Driver for Raspberry Pi (Raspbian OS / Kali)(ARM)</a><br>
  <a href="https://github.com/Krishak15/archer-t2u-plus-linux/edit/main/README.md#uninstall-driver-in-linux"> 3) Uninstall Driver in Linux</a><br/>
  <a href="https://github.com/Krishak15/archer-t2u-plus-linux/edit/main/README.md#troubleshooting"> 4) Troubleshooting</a>
</p>

TP-Link Archer T2U Plus a.k.a AC600 High Gain is a very **affordable** dual band wireless adapter **compatible with kali linux** and supports monitor mode , soft AP mode,packet injection etc. it supports both 2.4 GHz and 5GHz band and has a 5dBi Antenna for better signal reception. 2357:0120

<p align = "center">
<img src="https://github.com/nlkguy/archer-t2u-plus-linux/blob/main/Images/archer-t2u-inside.jpeg" alt="Retail Box" width="40%" height="40%">
</p>

## Why should i buy this adapter ?

This adapter has a **Realtek RTL8821AU Chipset** at its heart. RTL8821AU has plenty of developer support in linux community and has driver for Kali linux , Parrot OS .etc Archer T2U Plus is on sale **under 15 USD ~ 1000 INR** , which is a very affordable price for Beginners in Pentesting. 2357:0120 is the USB ID.

## Where to buy
:point_right:  [**Amazon**](https://amzn.to/3aPjBir)  
:point_right:  [**Flipkart**](https://dl.flipkart.com/dl/tp-link-ac600-t2u-plus-usb-adapter/p/itmfhz7zg85hgtzg?marketplace=FLIPKART&iid=79034678-e8a7-4d71-8d97-073f9497fcdc.USBFHZ7ZPWFHW8YW.SEARCH&ppt=sp&lid=LSTUSBFHZ7ZPWFHW8YW9SRRQK&srno=s_1_1&qH=2fca2860d6b488dc&pid=USBFHZ7ZPWFHW8YW&affid=amaledasse&ssid=7o14gihn8ag5p98g1609082867282&otracker1=search&ppn=sp)


## Driver for Debian Based Linux Distros (Ubuntu/Kali Linux)(x86_64)

1. Update the package information :
>```sudo apt update```
2. Install `dkms` and `git` :
>```sudo apt install dkms git```
3. Install Build Dependencies :
>```sudo apt install build-essential libelf-dev linux-headers-$(uname -r)``` 
4. Download the Driver files using `git` :
>```git clone https://github.com/aircrack-ng/rtl8812au.git```
5. Navigate to the Downloaded directory :
>```cd rtl88*```
6. Install the Driver 
>```sudo make dkms_install```

if the installation is aborted , check existing dkms modules and uninstall previously installed driver 

:point_right: [Uninstall Existing Driver](https://github.com/nlkguy/archer-t2u-plus-linux#uninstall-driver-in-linux)

7. Check the wireless interfaces by typing `iwconfig`.
<img src="https://github.com/nlkguy/archer-t2u-plus-linux/blob/main/Images/lsusb%3Biwconfig.png" alt="lsusb&iwconfig_result" width="50%" height="50%">

if you encounter any weird interface name , rename the Wireless interface by following below steps

:point_right: [Change/Rename Network Interface](https://github.com/nlkguy/archer-t2u-plus-linux/blob/main/change_interface_name.md)


## Driver for Raspberry Pi (Raspbian OS / Kali)(ARM)

1. Update the package information :
>```sudo apt update```

2. Install `dkms` and `git` :
>```sudo apt install dkms git```

3. Install Build Dependencies :
#### For Raspbian OS
>```sudo apt-get install raspberrypi-kernel-headers```

#### For Kali for ARM
>```sudo apt-get install build-essential libelf-dev kalipi-kernel-headers```

4. Download the Driver files using `git` :
>```git clone https://github.com/aircrack-ng/rtl8812au.git```

5. Navigate to the Downloaded directory :
>```cd rtl88*```

#### For Raspberry (RPI)

6. Then run this step to change platform in Makefile, For RPI 1/2/3/ & 0/Zero:

>```sed -i 's/CONFIG_PLATFORM_I386_PC = y/CONFIG_PLATFORM_I386_PC = n/g' Makefile```  
>```sed -i 's/CONFIG_PLATFORM_ARM_RPI = n/CONFIG_PLATFORM_ARM_RPI = y/g' Makefile```

#### But for RPI 3B+ & 4B you will need to run those below which builds the ARM64 arch driver:

>```sed -i 's/CONFIG_PLATFORM_I386_PC = y/CONFIG_PLATFORM_I386_PC = n/g' Makefile```  
>```sed -i 's/CONFIG_PLATFORM_ARM64_RPI = n/CONFIG_PLATFORM_ARM64_RPI = y/g' Makefile```

#### In addition, if you receive an error message about ```unrecognized command line option ‘-mgeneral-regs-only’``` (i.e., Raspbian Buster), you will need to run the following commands, then retry building and installing:

>```export ARCH=arm```  
>```sed -i 's/^MAKE="/MAKE="ARCH=arm\ /' dkms.conf```

7. Install the Driver 
>```sudo make dkms_install```
<img src="https://github.com/nlkguy/archer-t2u-plus-linux/blob/main/Images/kali-arm-installing.png" alt="Kali-ARM-RPi-Installing" width="70%" height="70%">

8. Check the wireless interfaces by typing `iwconfig`.

:point_right: [Change/Rename Network Interface](https://github.com/nlkguy/archer-t2u-plus-linux/blob/main/change_interface_name.md)

## Uninstall Driver in Linux

- check the module name and version using the command ```sudo dkms status.```  </br>  
  ```
  $ dkms status  
  8812au, 5.6.4.2_35491.20191025, 5.10.63+, armv6l: installed  
  rtl8188fu, 1.0, 5.10.63+, armv6l: installed.```  

- here module name is ```8812au``` and module version is ```5.6.4.2_35491.20191025```.

- use ```sudo dkms remove <module>/<module-version>.```  </br>  
  ```
  $ sudo dkms remove 8812au/5.6.4.2_35491.20191025 --all  
  
  Deleting module version: 5.6.4.2_35491.20191025 completely from the DKMS tree.  
  
  Done.  
  ```

- delete this file using  ```sudo rm -rf /var/lib/dkms/8812au/```.

## Troubleshooting
On Raspberry Pi 4 and Debian 10 image with kernel `5.10.103-v7l+`, I get this error.
```txt
user@pc:~/rtl8812au $ sudo make dkms_install                    
cp -r * /usr/src/8812au-5.6.4.2_35491.20191025                                        
1dkms add -m 8812au -v 5.6.4.2_35491.20191025                               
                                                                                        
Creating symlink /var/lib/dkms/8812au/5.6.4.2_35491.20191025/source ->
                 /usr/src/8812au-5.6.4.2_35491.20191025
                                               
DKMS: add completed.          
dkms build -m 8812au -v 5.6.4.2_35491.20191025
Error! echo
Your kernel headers for kernel 5.10.103-v7l+ cannot be found at
/lib/modules/5.10.103-v7l+/build or /lib/modules/5.10.103-v7l+/source.
make: *** [Makefile:1786: dkms_install] Error 1
```
In my case, there is a build directory, but it was empty.
I added a symbolic link in `/lib/modules/$(uname -r)` to the source files as follows:
```bash
rm -r /lib/modules/$(uname -r)/build
ln -s /usr/src/linux-headers-$(uname -r)/ /lib/modules/$(uname -r)/build
make dkms_install # now it works
```
## References
>[DigitalOcean.com : Sed Stream Editor Basics](https://www.digitalocean.com/community/tutorials/the-basics-of-using-the-sed-stream-editor-to-manipulate-text-in-linux)
