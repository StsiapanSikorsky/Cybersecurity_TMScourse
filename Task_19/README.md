# Домашнее задание 19: Основные виды СЗИ  
1) Установить антивирус ClamAV  
- Установить графическую оболочку  
- Просканировать любую директорию  

2) Установить YARA  
- Создать текстовый файл и вычислить его hash  
- Написать правило для детектирования данного файла  

3) *Установить WAF (nginx + Modsecurity)  
- Установить и протестировать запрет тестового запроса  

Ссылки на дополнительные ресурсы:   
- [Настройка Jump Server - Bastion](https://habr.com/ru/companies/cloud4y/articles/530516/)  
- [MDR архитектура от Kaspersky](https://support.kaspersky.com/MDR/ru-RU/196548.html)  
- [YARA installation and docs](https://yara.readthedocs.io/en/latest/gettingstarted.html)   
- [Nginx + Modsecurity WAF](https://opsshield.com/help/cpguard/install-modsecurity-with-nginx-on-debian-ubuntu/)  
- [Smirnov nginx + modsecurity github](https://github.com/sm1lexops/Profile_challenges?tab=readme-ov-file)  
- [NGFW free course](https://www.youtube.com/watch?v=uOMiC1-iwIc&list=PLqio-3dnMW5_2cStMfIezwcAzzDCjX86C)  

## 1) Установить антивирус ClamAV  
### 1.1 Установка и сканирование при помощи консоли
- Для установки бесплатного антивируса ClamAV на ВМ KaliLinux прописываем следующую команду  
>sudo apt install clamav clamav-daemon  

![ClamAV_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/ClamAV_1.png)

- Настраиваем автоматическое обновление баз антивируса
>sudo systemctl stop clamav-freshclam  
sudo freshclam  
sudo systemctl start clamav-freshclam  

![Warning_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/Warning_1.png)  

>[WARNING]
Как видно базы обновлены не были из за ошибки 403 и 429  
403 - стандартный код ответа HTTP, означающий, что доступ к запрошенному ресурсу запрещен.  
429 - пользователь отправлял чересчур много запросов за единицу времени. 

При заходе на официальный сайт [https://www.clamav.net/downloads](https://www.clamav.net/downloads) без подключения VPN, он блокируется  
![Warning_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/Warning_2.png)

- Сканирование файла
>clamscan dict.txt  

![ClamAV_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/ClamAV_3.png)  

- Сканирование не удалось, из за отсутствия баз данных.

- Опытным путем проб и ошибок был удален файл freshclam.dat из директории **/var/lib/clamav**, после чего была выполнена корректно выполненная команда **freshclam** (с подключенным VPN) 

![ClamAV_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/ClamAV_4.png)  

- В результате выполнено сканирование файла  
>clamscan файл  

![ClamAV_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/ClamAV_5.png)

- Сканирование директории  
>clamscan директория  

![ClamAV_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/ClamAV_6.png)  

### 1.2 Установка и сканирование при помощи GUI   
- Установка выполняется при помощи команды  
>sudo apt install clamtk  

![ClamAV_7](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/ClamAV_7.png)  

Главное окно программы ClamTk  
![ClamAV_8](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/ClamAV_8.png)  

- Сканирование файла ClamTk  

![ClamAV_9](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/ClamAV_9.png)  

- Сканирование директории с утилитой xerxes  

![ClamAV_10](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/ClamAV_10.png)  

## 2) Установка YARA  

