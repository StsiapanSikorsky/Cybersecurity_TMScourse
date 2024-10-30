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

![OpenVAS_1]()  

- Проверям и запускаем службу **Redis**, скаченную вместе с OpenVAS:  

>sudo systemctl status redis-server@openvas.service  
sudo systemctl enable redis-server@openvas.service

![OpenVAS_2]()  

- Запускаем настройки **gvm**, необходимого для создания пользователя OpenVAS

>sudo gvm-setup  

![OpenVAS_3]()  

>[!CAUTION] При создании обязательно запомнаем сгенерированный пароль для пользователя **admin**, в нашем случае: 89305172-46f7-4058-a4cf-5fd76177ecf9

- Проверяем правильность настройки:

>sudo gvm-check-setup  

![OpenVAS_4]()  

- Обновляем каналы:  

>sudo greenbone-feed-sync  

- Запускаем OpenVas, при этом браузер открывается автоматически на **http://127.0.0.1:9392**    

>sudo gvmd  
sudo ospd-openvas  
sudo gvm-start

![OpenVAS_5]() 

- Вводим ранее сгенерированный пароль и логин admin, проваливаемся в сканнер  

![OpenVAS_6]()  

### 1.2 Сканирование системы при помощи OpenVAS  


