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

![BASH_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_26/img/BASH_1.png)  

## 2) Написать PowerShell-script  
### 2.1) Изучение PowerShell

Командлет - команды, встроенные в PowerShell. Имеют систему наименования **Глагол-Объект**    

- Список папок в текущем каталоге  (3 варианта)  
``` powershell
dir  
```   

``` powershell
ls  
```   

``` powershell
Get-ChildItem
```   

- Вывести список всех алиасов  
``` powershell
ls Alias:\
```   

- Получить список процессов  
``` powershell
Get-Process
```   

- Удаление чего либо  
``` powershell
Remove-Item  
```   

- Получение справки  
``` powershell
Get-Help  
get-help files
get-help new-item -Examples
```   

``` powershell
Get-ChildItem
```   

- Создание нового алиаса  
``` powershell
Set-Alias  
```   

- Создать овый объект (файли и т п)  
``` powershell
New-Item  
```   

- Просмотр дисков системы  
``` powershell
Get-PSDrive  
```   

- Хождение по системе (аналог cd)  
``` powershell
Set-Location D:\Program....  
```   

- Вывод списка файлов с определенным расширением (+ | вывод данных файла)    
``` powershell
ls -filter "*jpg" | Get-Content
```   
- Список процессов, запущенных в системе  
``` powershell
ps  
```   

- Создание переменной и получение ей данных сервера  
``` powershell
$value.DownloadString("http://google.com")  
```   

- Вывод в консоль (вторая команда по конвееру)
``` powershell
Write-Host "Hello"  
Write-Output "Hello for conveer"  
```   

### 2.2) Скрипты на PowerShell

- Пример скрипта по выводу места на ЖД компьютера  
``` powershell
Get-WmiObject -Class Win32_LogicalDisk | 
Select-Object -Property DeviceID, VolumeName, @{Label='FreeSpace (Gb)'; expression={($_.FreeSpace/1GB).ToString('F2')}},
@{Label='Total (Gb)'; expression={($_.Size/1GB).ToString('F2')}},
@{label='FreePercent'; expression={[Math]::Round(($_.freespace / $_.size) * 100, 2)}}|ft
```  

![PowerShell_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_26/img/Powershell_1.png)  
