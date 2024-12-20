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

## 1) Сканнер уязвимостей OpenVAS  
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

![OpenVAS_7](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenVAS_7.png)  

Так и при помощи своего созданного задания  

![OpenVAS_8](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenVAS_8.png)  

Результаты сканирования выполненые в интерактивном режиме 
>Scans->Reports->ЛКМ на ссылку в поле Task->Repult for Task (значок сверху)

![OpenVAS_9](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenVAS_9.png)  

### 1.3 Поиск устранения найденной уязвимости SSL/TLS: Report Weak Clier Suites

![OpenVAS_10](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenVAS_10.png) 

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



## 2) Регистрация и отслеживание актуальных уязвимостей на сайте [opencve.io](https://app.opencve.io/)  
- Для регистрации необходимо лишь ввести почту, юзернэйм и ввести пароль, после чего требуется подтверждение почты  
- После завершения процесса регистрации создаем пользователя, а также проект (появляется в разделе projects)  

![OpenCVE_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenCVE_1.png)

- В разделе Vendors & Products ищем и выбираем интересующие нас разделы и добавляем их в проект  

![OpenCVE_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenCVE_2.png)  

- В Dashbord можем найти актуальные новости уязвимостей по подписанным сервисам  

![OpenCVE_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/OpenCVE_3.png) 

## 2) PatrOwl  
PatrOwl - бесплатное, масштабируемое, открытое решение для оркестровки операций безопаности (сканирование, поиск, вызовы API).  

### 2.1 Установка PatrOwl  

Выполняем перечень команд:  
1) Загрузка PatrOwl с github  
>git clone https://github.com/Patrowl/PatrowlManager.git  

2) Развертываем back-end при помощи docker  
>cd PatrowlManager  
docker-compose build --force-rm  
docker-compose up  

При завершении переходим в браузер на http://localhosst:8083 и вводим учетные данные:  
Логин: admin  
Пароль: Bonjour1!  

![PatrOwl_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/PatrOwl_1.png)  

Главное окно Frontend PatrOwl  

![Patrowl_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/Patrowl_2.png)  

### 2.2 Функционал PatrOwl  
Для добавления актива следует в хэдере перейти во вкладку Assets и выбрать Add new asset  

![PatrOwl_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/PatrOwl_3.png)  

В открывшемся окне выбираем нужные нам параметры  

![PatrOwl_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/PatrOwl_4.png)  

Для добавления движка следует в хэдере перейти во вкладку Engines и выбрать Add scan engine instance  

![PatrOwl_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/PatrOwl_5.png)  

В открывшемся окне выбирраем нужные параметры  

![PatrOwl_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/PatrOwl_6.png)  

Для добавления сканера следует в хэдере перейти во вкладку Scans и выбрать Add new scan  

![PatrOwl_7](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/PatrOwl_7.png)  

В открывшемся окне выбирраем нужные параметры (задаем созданный актив, выбираем созданный движок на основе NMAP)  

![PatrOwl_8](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_22/img/PatrOwl_8.png)  

