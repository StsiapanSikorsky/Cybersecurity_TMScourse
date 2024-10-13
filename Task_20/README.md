# Домашнее задание 20: Основный виды СЗИ  
1) Установка и тестирование Suricata IDS  
- Установка Suricata  
- Добавить правило FIN or SIN сканирования в suricata  
- Перезагрузить suricata  
- Запустить kali linux и просканировать виртуалку suricata  
- Предоставить скрины и лог файла suricata при сканировании  

Ссылки на дополнительные ресурсы:  
- [Fail to ban - анализ лога и блокировка](https://github.com/fail2ban/fail2ban)   
- [Hydra - инструмент подбора паролей, bruteforce](https://github.com/vanhauser-thc/thc-hydra)  
- [Suricata - сетевая IDS система](https://suricata.io/)  
- [Suricata - документация](https://docs.suricata.io/en/suricata-6.0.2/)  
- [Windows Defender - что это и как с ним раотать](https://journal.tinkoff.ru/windows-defender/)  
- [Passwords and Users database](https://github.com/danielmiessler/SecLists/blob/master/Usernames/xato-net-10-million-usernames-dup.txt)  

## 1) Установка и тестирование Suricata IDS 
>[!NOTE]
Suricata - программный комплекс для сбора, аудита и мониторинга сетевой безопасности. Утилита анализирует весь поступающий трафик на основе правил (предопределенных или пользовательских)  

### 1.1 Установка Suricata
- Для установки **suricata** требуется выполнить команду:  
>sudo apt install suricata  

![Suricata_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_20/img/Suricata_1.png)  

- Добавляем программу в системный пул с автозапуском:  
>systemctl enable suricata  

![Suricata_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_20/img/Suricata_2.png)  

- Редактирование правил **suricata** происходит в конфигурационном **suricata.yaml** файле находящемуся по пути: /etc/suricata  

![Suricata_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_20/img/Suricata_3.png)  

- Список протоколов подлежащих проверке на уровне приложений можем получить используя команду:  
>sudo suricata --list-app-layer-protos  

![Suricata_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_20/img/Suricata_4.png)  



## 1.2 Перезапуск службы suricata  
- Для перезапуска службы и проверки используем команды:  
>systemctl restart suricata  
systemctl status suricata  

![Suricata_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_20/img/Suricata_5.png)  


## 1.3 Предварительная настройка и сканирование KaliLinux   
- Перед начаом скнирования обновляем файлы **suricata**:  
>sudo suricata-update  

![Suricata_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_20/img/Suricata_6.png)  

- Проверяем суриката в режиме тестирования (если всё впорядке, получаем только сообщение о версии):
>sudo suricata -Tc /etc/suricata/suricata.yaml  

![Suricata_7](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_20/img/Suricata_7.png)  

- Запускаем **suricata** в режиме IDS:   
>sudo suricata -c /etc/suricata/suricata.yaml -i eth0  

![Suricata_8](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_20/img/Suricata_8.png)  

- Для запуска **suricata** в режиме IPS:  
>sudo suricata -c /etc/suricata/suricata.yaml --af-packet -D  

- Файлы логов находятся в дериктории **/var/log/suricata/**  

![Suricata_9](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_20/img/Suricata_9.png)  

![Suricata_10](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_20/img/Suricata_10.png)  


