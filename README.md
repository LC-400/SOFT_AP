Soft AP with hostapd. Host: 

Tested successfully on Raspberry PI Zero. Scanning device: Samsung Galaxy III.


The AP announces its presence with power reading and public name.

Required steps for installation and configuration of hostapd service:
Obtain package hostapd (apt-get install hostapd). 
Configuration file is located in: /etc/hostapd/hostapd.conf
Stop hostapd-service before configuration:systemctl stop hostapd
Configure interface, driver, channel, wpa passphrase, SSID etc.
Configure the hostapd-service: configure_hostapd

start the AP: start_ap
stop the hostapd-service:stop_ap

Required steps for configuring network device:
Set static IP for desired device (e.g Wlan0) (/etc/network/interfaces)
Check device for AP-mode: check_mode

Please observe: The hostapd-service is particular about a minimum passphrase-length
of 8 letters.

To access the Internet via the AP:
Uncomment net.ipv4.ip_forward=1 (/etc/sysctl.conf)
Add a masquerade for outbound traffic on wlan0 and save iptables: add_masq

Preserve iptables across boot:
Add "iptables-restore < /etc/iptables.ipv4.nat" (/etc/rc.local, above "exit 0")

Files:
configure_hostapd
check_mode
start_ap
stop_ap
add_masq

