# Домашнее задание 9 - Социальная инженерия, фишинг

**1) Разослать фишинговое письмо с уникальной информацией, ведущее на копию крупного ресурса (соцсети, почты и т.д.)**  
- установить setoolkit на ВМ KaliLinux;
- создать фишинговую копию сайта;  
- сделать фишинговое письмо с копией распространенного сервиса;  
- сделать скрин сервиса, и перехват данных авторизации;  
- *сделать все это на ВМ в облаке с привязкой к реальному домену.  

### Ссылки на дополнительные ресурсы
[Github repo setoolkit](https://github.com/trustedsec/social-engineer-toolkit)  
[Установка setolkit на Ubuntu](https://www.youtube.com/watch?v=y4sIesUADD8&themeRefresh=1)

## 1) Установка setoolkit на Ubuntu
- Клонируем репозиторий setoolkit в созданную нами папку
>sudo git clone https://github.com/trustedsec/social-engineer-toolkit /setoolkit

- Заходим в папку с репозиторием и начинаем установку **setoolkit**  
>cd /setoolkit  
>pip3 install -r requirements.txt  

![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task9/img/install_setoolkit.png)   

>python3 setup.py

![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task9/img/install_setoolkit_2.png)  

- Запускаем setoolkit  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task9/img/setoolkit_start.png)

## 2) Фишинговый сайт
- Для осуществления атаки при помощи копии сайта запускаем setoolkit и переходим по ветви

> 1) Social-Engineering Attack -->  
> 2) Webside Attack Vectors -->
> 3) Credential Harvester Attack Method -->
> 2) Site Cloner  

- Для копирования был выбран сайт Kufar.by. Сайт был успешно скопирован, о чем свидетельствует его айпи адрес в верхнем левом углу   
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task9/img/kufar.png)

- Атака через сайт Kufar.by не увенчалась успехом, поскольку пользователю для ввода логина и пароля требовалось пройти капчу
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task9/img/kufar_capcha.png)   

## 3) Рассылка фишинговых писем
- Для рассылки фишинговых писем первоначально организовывается взаимоджействие с почтовым ящиком, с которого осуществляется рассылка, для этого в управлении аккаунта гугл (был использован @gmail) в строке поиска находим пароли приложений и вводим название приложения
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task9/img/Authentication1.png)

- Как результат получаем пароль для осуществления аунтефикации
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task9/img/Authentication2_password.png)

>[!ATHENTION]
>Для использования данного пароля, необходимо чтобы в аккаунте Гугл была подключена двухэтапная аутентификация

- Далее в терминале запускаем seetoolkit и для осуществленния данного типа атаки переходим по ветви:  
> 1) Social-Engineering Attack -->  
> 5) Mass Mailer Attack -->
> 1) E-Mail Attack Single Email Address -->
> 1) Pre-Defined Template -->
> 2) number message -->

- Путем задания дополнительных параметров (ящика атакуемого, ящика атакующего и ключа аутентификации от ящика) выполняем атаку  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task9/img/EmailSpam_Console.png)

- Проверяем письмо полученное на ящик атакуемого
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task9/img/EmailSpam_Result.png)

- Также просмотрим отправленные письма с ящика атакующего
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task9/img/EmailSpam_SendAddress.png)

