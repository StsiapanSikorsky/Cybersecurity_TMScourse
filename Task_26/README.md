# Домашнее задание 26: Scripting   
1) Написать интерактивный bash-script для автоматизации часто повторяемых действий (обновление пакетного менеджера, установка wget, curl, docker, docker-compose)  
- *написать скрипт с интерактивным выбором установленного ПО  
- *если пакет установлен вывести сообщение, что утилита установлена и предложить установить другие утилиты  

2) Написать PowerShell-script  
- Инсталяция каких-либо программ, вывод подробной информации о системе (свободное место на дисках, ram, cpu и тд)   

Дополнительные ресурсы:  
- ![bash-script примеры использования](https://habr.com/ru/companies/ruvds/articles/325522/)  
- ![powershell-scripts примеры использования](https://habr.com/ru/articles/113913/)  

## 1) Скрипт на bash для подключения VPN соединения  
``` bash
#!/bin/bash  
RED='\033[0;31m'  
GREEN='\033[0;32m'  
RESET='\033[0;0m'  

echo -e "$GREEN loading OpenVPN $RESET"  
sudo apt install openvpn  

echo -e "$GREEN VPN connect... $RESET"  
echo -e "$GREEN Input port VPN-connection $RED 443, 80, 53, or 25000 $RESET"  

cd ~/Downloads/vpnbook-openvpn-ca196  

read -p "Number port =" valuePort  

if [ "valuePort" -eq 443 ]; then
    echo -e "$GREEN Port 443: Input username $RED vpnbook $GREEN and input password $RED e81zu76 $RESET"  
    sudo openvpn vpnbook-ca196-tcp443.ovpn  
elif [ "valuePort" -eq 80 ]; then
    echo -e "$GREEN Port 80: Input username $RED vpnbook $GREEN and input password $RED e81zu76 $RESET"  
    sudo openvpn vpnbook-ca196-tcp80.ovpn
elif [ "valuePort" -eq 53 ]; then
    echo -e "$GREEN Port 53: Input username $RED vpnbook $GREEN and input password $RED e81zu76 $RESET"  
    sudo openvpn vpnbook-ca196-udp53.ovpn
elif [ "valuePort" -eq 25000 ]; then
    echo -e "$GREEN Port 25000: Input username $RED vpnbook $GREEN and input password $RED e81zu76 $RESET"  
    sudo openvpn vpnbook-ca196-udp25000.ovpn    
else  
    echo -e "$RED Input incorrect port $RESET"
    exit
fi  

echo -e "$GREEN VPN-connect is complete  
``` 

- Для автоматического вызова по названию перемещаем скрипт в директорию /usr/local/bin  

>sudo mv VPN.sh /usr/local/bin  

- Результат выполнеия скрипта (установление VPN соединения)  

![BASH_1]()
