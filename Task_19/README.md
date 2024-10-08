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

>![WARNING]
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

>![NOTE]
YARA - утилита позволяющая выполнять сигнатурный анализ на основе YARA описаний (правил). В них содер­жатся инди­като­ры ком­про­мета­ции для раз­ных типов вре­донос­ного ПО  

### 2.1 Установка YARA  
- Установка выполняется следующей командой  
>sudo apt install yara  

![Yara_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/Yara_1.png)  

### 2.2 Вычисления хэш суммы файла   
- Для вычисления хэш суммы используют название соответсвующей хэш-функции, для примера был вычеслен хэш SHA256 и MD5 скрипта script1.sh  
>sha256sum script1.sh    
md5sum script1.sh  

![Yara_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/Yara_2.png)  

### 2.3 Написания правила YARA для детектирования файла по хэш функции
- Создаем правило, при этом расширение ставим **.yar**  

Правило YARA начинается с **rule** за которым следует его название, далее сами правила описываются в **"{}"**.  

Первым блоком следуют метаданные в которых описывается различная полезная информация (автор, дата создания, версия и т.д.)  

Вторым блоком описываются переменные, найденные во вредоносном файле (в нашем случае хэш файла)  

Третий блок представляет собой условия, необхоимые для срабатывания правила  

- В нашем случае при написании правила используем специальную функцию hash.md5(0, filesize) для срабатывания правила по хэшу файла  

![Yara_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/Yara_4.png):

- Результат, обнаружение вредоносного файла  

![Yara_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_19/img/Yara_5.png);  

