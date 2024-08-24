~to check the information on supplemental access points do this command

$ systemctl status wpa_supplicant.service

~To further validate our understanding, we will now investigate the presence of the hostap service.
Hostap is commonly used in routers and Android phones to create and manage Access Points. 

$ systemctl status hostapd.service

To enumerate wireless network interfaces

$ iwconfig