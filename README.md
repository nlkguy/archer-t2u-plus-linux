# TP-Link Archer T2U Plus a.k.a AC600 High Gain

TP-Link Archer T2U Plus a.k.a AC600 High Gain is a very **affordable** dual band wireless adapter **compatible with kali linux** and supports monitor mode , soft AP mode,
packet injection etc. it supports both 2.4 GHz and 5GHz band and has a 5dBi Antenna for better signal reception.

## Why should i buy this adapter ?
This adapter has a **Realtek RTL8821AU Chipset** at its heart. RTL8821AU has plenty of developer support in linux community and has driver for Kali linux , Parrot OS , Black Arch .etc
Archer T2U Plus is on sale **under 15 USD ~ 1000 INR** , which is a very affordable price for Beginners in Pentesting.

## Driver Installation for Debian Based Linux Distros (Ubuntu/Kali Linux)

1. Update the package information :
>```sudo apt update```
2. Install `dkms` package :
>```sudo apt install dkms```
3. Download the Driver files using `git` :
>```git clone https://github.com/aircrack-ng/rtl8812au.git```
4. Install Build Dependencies :
>```sudo apt install build-essential libelf-dev linux-headers-$(uname -r)``` 
5. Navigate to the Downloaded directory :
>```cd rtl88*```
6. Install the Driver 
>```sudo make dkms_install```
