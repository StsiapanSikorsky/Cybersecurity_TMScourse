# Домашнее задание 18: Защита инфраструктуры приложений Ч2  
1) Установить 2FA (двухфакторную аутентификацию) на linux (Google authenticator)  
- Скрин о запросе кода авторизации  
2) any.run  
- Регистрируемся, тестим ссылки и файлы в sandbox  

Ссылки на дополнительные ресурсы:  
- [Dynamic Access Control в Windows Server](https://winitpro.ru/index.php/2013/01/24/dynamic-access-control-v-windows-server-2012/)  
- [Настройка 2FA для SSH Linux](https://dzen.ru/a/Yo052tNMkSmr3U9o)  
- [Configure 2FA on Ubuntu](https://www.linuxbabe.com/ubuntu/two-factor-authentication-ssh-key-ubuntu)   
- [ANY.RUN sandbox и анализ уязвимостей](https://any.run/)  
- [Примеры различных Honeypot](https://habr.com/ru/companies/bastion/articles/731172/)  
- [Как повысить привилегии LotL attack and GFtoBINS](https://habr.com/ru/companies/oleg-bunin/articles/799773/)  

## 1) Установка 2FA (Google authenticator) на KaliLinux  
- Установка модуя Google authenticator PAM выполняем при помощи следующей команды  
>sudo apt install libpam-google-authenticator  

![GoogleA_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_18/img/GoogleA_1.png)  

- Редактируем файл /etc/pam.d/sshd путем добавления в него строки  
>auth required pam_google_authenticator.so

![GoogleA_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_18/img/GoogleA_2.png)  

- Выполняем перезагрузку службы sshd  
>sudo systemctl restart sshd.conf  

- Редактируем файл /etc/ssh/sshd_conf путем добавления в него строки  
>KbInteractiveAuthentication yes  

![GoogleA_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_18/img/GoogleA_3.png)  

- Выполняем перезагрузку службы sshd  
>sudo systemctl restart sshd.conf  

- Настраиваем аутентификацию, прописываем команду  
>google-authenticator  

![GoogleA_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_18/img/GoogleA_4.png)  

- Отвечаем на вопросы google-authenticator  
    Сделать токены аутентификации привязанными по времени (да / нет): y  
    Обновить файл » ~ / .google_authenticator » (y / n): y  
    Запретить многократное использование одного и того же токена аутентификации ?: y  
    Увеличить частоту генерации кода (y / n):  n    
    Включить ограничение скорости (да / нет): y  

![GoogleA_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_18/img/GoogleA_5.png)  

- Устанавливаем приложение **Google Authenticator** на смартфон и подключаем устройство по QR-коду (либо по коду ниже)  

![GoogleA_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_18/img/GoogleA_6.png)  

## 2) any.run 
Ввиду отсутствия корпоративной почти, изучение не было выполнено
