# Change Network Interface Name
I've encountered a weird and long interface name after [installing drivers for my TP-Link Archer T2U Plus](https://github.com/nlkguy/archer-t2u-plus-linux/blob/main/README.md) USB Wifi Adapter in My Linux Machine. 
It was shown up as **"wlx984827a0287e"** in the result of `ifconfig` or `iwconfig`. I was only familiar with names like wlan0,wlan1,wlp1s0 .etc 
So i changed **"wlx984827a0287e"**. Smaller is sometimes better  :smile: .  Here is how i did it.

<img src="https://github.com/nlkguy/archer-t2u-plus-linux/blob/main/Images/lsusb%3Biwconfig.png" alt="lsusb&iwconfig_result" width="50%" height="50%">

## Steps to change Interface name

Disable [predicatble Network Interface names](https://wiki.archlinux.org/index.php/Network_configuration#Reverting_to_traditional_device_names)

1. Edit your grub configuration file:

>```sudo nano /etc/default/grub```

Add ```net.ifnames=0 biosdevname=0 to GRUB_CMDLINE_LINUX=""```  
like this:```GRUB_CMDLINE_LINUX="net.ifnames=0 biosdevname=0"```

2. Update grub.cfg :

>```sudo grub-mkconfig -o /boot/grub/grub.cfg```

Find the MAC Address of Network Interfaces

3. >`ifconfig`  
Copy the 12 digit MAC address preciding 'ether' usually in the 4th line .

4. Create the configuration file (70-persistent-net.rules) :

> ```sudo touch /etc/udev/rules.d/70-persistent-net.rules```  
> ```sudo nano /etc/udev/rules.d/70-persistent-net-rules```  you can use any text editor of choice instead of `nano`

5. Add the following line per interface. Add the MAC address and the new NAME per interface.

>SUBSYSTEM=="net", ACTION=="add", DRIVERS=="?*", ATTR{address}=="{insert MAC Address Here.remove curls}", ATTR{dev_id}=="0x0", ATTR{type}=="1", KERNEL=="eth*", NAME="wlan0"  
>SUBSYSTEM=="net", ACTION=="add", DRIVERS=="?*", ATTR{address}=="{insert MAC Address here.remove curls}", ATTR{dev_id}=="0x0", ATTR{type}=="1", KERNEL=="eth*", NAME="wlan1"  

6. Save the file and reboot.

<img src="https://github.com/nlkguy/archer-t2u-plus-linux/blob/main/Images/interface-name-change.png" alt="Final-Changed-name" width="50%" height="50%">


### References
[Mellanox Community](https://community.mellanox.com/s/article/howto-change-network-interface-name-in-linux-permanently)  
[Stack Exchange](https://unix.stackexchange.com/questions/328485/ubuntu-16-04-change-interface-name)  
[Shellhacks.com](https://www.shellhacks.com/change-network-interface-name-eth0-eth1-eth2/)
