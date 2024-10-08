 # Домашнее задание 3 - KaliLinux
 1) **Установка на ВМ Windows10/WindowsServer SSH Server и его запуск**
 2) **Разрешение подключение по RDP**
 3) **Сканирование подсети с ВМ KaliLinux**
 4) **BrudeForce (ssh) пароля от ВМ Windows10**

 ## 1) Установка на ВМ Windows10 SSH Server
 - Установка SSH Server  
 ![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task3/img/installSSHserv_Win10.png)

 - Запуск SSH Server  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task3/img/StartSSHserver_Win10.png)

- Проверка работы SSH Server на ВМ Windows10 путем подключения с KaliLinux  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task3/img/Connect_SSH_Win10.png)  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task3/img/SSH_Win10.png)

## 2) Разрешение подключения по RDP
- Для разрешения подключения на Windows 10 по RDP необходимо перейти в: "Пуск-Настройки-Система-Удаленный рабочий стол-Включить удаленный рабочий стол"  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task3/img/RDP.png)

## 3) Сканирование сети при помощи NMap (KaliLinux)
- Полное сканирование при помощи nmap  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task3/img/NMap_resultScan.png)  

- Сканирование определенного адреса с утилитой -Pn (считать что машина включена)  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task3/img/NMap_scanning.png)

## 4) BrudeForce ВМ Windows10
- Создание словаря паролей (цифровых трехзнычных) с использованием CRUNCH  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task3/img/Crunch_generated.png)

В результате формируется документ dict2.txt содержащий словарь цифровых паролей от 1 до 3 знаков

- Проведение атаки на Windows 10 (username:stepa password:51) при помощи HYDRA  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task3/img/Hydra_correct_password.png)
