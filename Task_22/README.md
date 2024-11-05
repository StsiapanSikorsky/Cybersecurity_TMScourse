# Домашнее задание 22: Vulnerability assessment  
1) Scanner OpenVAS  
- установить сканер уязвиостей OpenVAS  
- просканировать VM  
- из отчета выбрать CVE и на различных ресурсов найти решение по устранению уязвимости  

2) Зарегестрироваться на opencve.io  
- подписаться на отслеживание релевантных для себя уязвимостей (Linux, Windows, сетевое обоорудование и т.д.)  

3) Установить PatrOwl  
- добавить несколько активов, рассмотреть функционал решения  

Ссылки на дополнительные ресурсы  
- [nvd.nist.gov](https://nvd.nist.gov/)  
- [opencve.io](https://www.opencve.io/welcome)
- [vulners.com](https://vulners.com/)  
- [otx.alienvault.com](https://otx.alienvault.com/)  
- [OpenVAS видео](https://www.youtube.com/watch?v=egiJ9A7oq3U)  
- [PatrOwl установка](https://github.com/Patrowl/PatrowlDocs/blob/master/installation/installation-guide.md)  
- [Greenbone VM](https://www.greenbone.net/en/greenbone-free/)    

## Сканнер уязвимостей OpenVAS  
### 1.1 Установка OpenVAS  
- Для установки выполняем команду:

>sudo apt install openvas -y  

![OpenVAS_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenVAS_1.png)  

- Проверям и запускаем службу **Redis**, скаченную вместе с OpenVAS:  

>sudo systemctl status redis-server@openvas.service  
sudo systemctl enable redis-server@openvas.service

![OpenVAS_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenVAS_2.png)  

- Запускаем настройки **gvm**, необходимого для создания пользователя OpenVAS

>sudo gvm-setup  

![OpenVAS_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenVAS_3.png)  

>[!CAUTION] При создании обязательно запомнаем сгенерированный пароль для пользователя **admin**, в нашем случае: 89305172-46f7-4058-a4cf-5fd76177ecf9

- Проверяем правильность настройки:

>sudo gvm-check-setup  

![OpenVAS_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenVAS_4.png)  

- Обновляем каналы:  

>sudo greenbone-feed-sync  

- Запускаем OpenVas, при этом браузер открывается автоматически на **http://127.0.0.1:9392**    

>sudo gvmd  
sudo ospd-openvas  
sudo gvm-start

![OpenVAS_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenVAS_5.png) 

- Вводим ранее сгенерированный пароль и логин admin, проваливаемся в GUI  

![OpenVAS_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenVAS_6.png)  

### 1.2 Сканирование системы при помощи OpenVAS  
Сканирование можно выполнять как в интерактивном режиме  

![OpenVAS_7]()  

Так и при помощи своего созданного задания  

![OpenVAS_8]()  

Результаты сканирования выполненые в интерактивном режиме 
>Scans->Reports->ЛКМ на ссылку в поле Task->Repult for Task (значок сверху)

![OpenVAS_9]()  

### 1.3 Поиск устранения найденной уязвимости SSL/TLS: Report Weak Clier Suites

![OpenVAS_10]() 

- CVE-2015-4000 (уязвимость обмена ключами DH)  
решение:  
1) Выполните следующую команду , чтобы увеличить размер ключа Диффи-Хеллмана до 4096 бит:
>plesk sbin sslmng -vvv --strong-dh --dhparams-size=4096  

- CVE-2013-2566 (уязвимость алгоритма RC4)  
решение: 
1) Прекратите использовать RC4 в качестве основного набора шифров в SSL/TLS.  
2) Переключитесь на наборы шифров режима CBC или режимы аутентифицированного шифрования, такие как наборы шифров AEAD TLS.  
3) Обновите браузеры для поддержки режимов аутентифицированного шифрования.  
4) Внедрите более жесткие ограничения на продолжительность и срок действия сеансовых cookie-файлов.  

- CVE-2015-2808 (уязвимость алгоритма RC4)  
решение: [https://nvd-nist-gov.translate.goog/vuln/detail/CVE-2015-2808?_x_tr_sl=en&_x_tr_tl=ru&_x_tr_hl=ru][https://nvd-nist-gov.translate.goog/vuln/detail/CVE-2015-2808?_x_tr_sl=en&_x_tr_tl=ru&_x_tr_hl=ru]  

Деактивация слабоко шифрования в SSL/TLS в Windows под управлением Active Directory следует использовать следующий алгоритм:  
1) Чтобы изменить объект групповой политики на сервере Active Directory, выберите Пуск > Администрирование > Управление групповой политикой , щелкните правой кнопкой мыши объект групповой политики и выберите Изменить.  
2) В редакторе управления групповыми политиками перейдите в раздел Конфигурация компьютера > Политики > Административные шаблоны > Сеть > Параметры конфигурации SSL.  
3) Дважды щелкните «Порядок набора шифров SSL».  
4) В окне «Порядок набора шифров SSL» нажмите «Включено».  
5) На панели «Параметры» замените все содержимое текстового поля «Наборы шифров SSL» следующим списком шифров:  
>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,  
TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,  
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,  
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,  
TLS_DHE_RSA_WITH_AES_128_GCM_SHA256,  
TLS_DHE_RSA_WITH_AES_256_GCM_SHA384,  
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384,  
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA,  
TLS_DHE_RSA_WITH_AES_128_CBC_SHA256,  
TLS_DHE_RSA_WITH_AES_256_CBC_SHA256  
6) Выйдите из редактора управления групповой политикой.  
7) Чтобы новая групповая политика вступила в силу, перезагрузите компьютеры Horizon Agent.  









