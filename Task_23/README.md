# Домашнее задание №23: Event Management  

1) Изучение лабораторных стенодов Splunk SIEM   
- [Лабораторная практика c SIEM систаемами](https://cyberdefenders.org/)  
2) Установка EFK стэка с помощью docker-compose  
- [Установка EFK](https://docs.fluentd.org/container-deployment/docker-compose)  
3) *Установка SIEM Wazuch с помощью docker-compose  
- [Установить Wazuch docker-compose](https://documentation.wazuh.com/current/deployment-options/docker/docker-installation.html)  

Ссылки на дополнительные ресурсы  
- [Сравнение SIEM систем](https://www.anti-malware.ru/compare/SIEM-systems)  
- [Работа auditd linux](https://www.redhat.com/sysadmin/configure-linux-auditing-auditd)  
- [Лабораторная практика с SIEM системами](https://cyberdefenders.org/)  
- [Pozitive портал обучения](https://lms.edu.ptsecurity.com/)  

## 1) Лабораторные стены Splunk SIEM
### 1.1 ЛР1 - Packet detective lab  
Описание: анализ файлов перехвата сетевого трафика при помощи программы WireShark
- анализ превышеющей сессии обмена пакетами SMB  
- аутентификация пользователя через кого получен доступ  
- поиск службы через которую происходил обмен файлов  
- измерение продолжительности связи между двумя хостами  
- поиск имени злоумышленника  
- поиск названия исполняемого файла  

Полезные команды в WireShark  
>smb2.filename contains ".exe" - поиск файла по протоколу SMB2, c расширением .exe  
ip.addr == 10.1.30.46 - поиск по IP адресу  
tcp.port == 80 - поиск по порту  

Отчет о выполненой работе  
![Lab_1]()  


### 1.2 ЛР2 - Yellow RAT lab  
Описание: анализ в **Virus Total** вредоносного файла, по хэшу  
- поиск названия вредоносного ПО  
- поиск общего имени файла  
- определение времени компиляции вредоноса  
- поиск встраиваемых вредоносных файлов  
- поиск С2 сервера, на каторый вредонос отправляет данные  

Отчет о выполненной работе  
![Lab_2]()  



