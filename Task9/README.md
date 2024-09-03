# Домашнее задание 9 - Социальная инженерия, фишинг

**1) Разослать фишинговое письмо с уникальной информацией, ведущее на копию крупного ресурса (соцсети, почты и т.д.)**  
- установить setoolkit на ВМ KaliLinux;  
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

> 2) Webside Attack Vectors --> 3) Credential Harvester Attack Method --> 2) Site Cloner


