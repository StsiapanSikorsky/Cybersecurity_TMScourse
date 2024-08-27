# Лабораторная работа 1: Web cache deception (обман веб кеша)
## 1) Общие сведения  
Обман веб кеша - уязвимость, позволяющая злоумышленнику обманом заставить веб-кэш хранить конфиденциальный динамический контент

>[!IMPORTANT]  
Значения кэш заголовков:  
X-Cache:hit - ответ был отправлен из кэша     
X-Cache:miss - в кэше небыло ответа на ключ запроса, поэтому ответ получен с исходного сервера     
X-Cache:dynamic - исходный сервер динамически генерировал контент (ответ не подходит для кэширования)    
X-Cache:refresh - кэшированное содержимое устарели и его необходимо обновить или повторно проверить  

## 2) Ход выполнения работы  

Ссылка на лабораторную работу: [Использование сопоставления путей для обмана веб-кэша](https://portswigger.net/web-security/web-cache-deception/lab-wcd-exploiting-path-mapping)  

### 2.1 
Логинимся под известным пользователем и смотрим ответ сервера (было найдено что ключ API явно передается в коде HTML страницы)   
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Lab_PortSwigger/Lab1_WebChacheDeception/img/labCache_1.png)  

### 2.2  
Пробуем обратитья к кэшу, для его проверки, путем добавления названия "123.js". В результате получаем ответ от сервера, так как кэш оказался пустой  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Lab_PortSwigger/Lab1_WebChacheDeception/img/labCache_2.png)  

### 2.3  
Повторно отправляем кэш запрос и получаем ответ из кэша (X-Cache: hit)  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Lab_PortSwigger/Lab1_WebChacheDeception/img/labCache_3.png)

### 2.4
Переходим в раздел внедрения эксплоита и копируем путь, изменяя файл находящийся в кэше  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Lab_PortSwigger/Lab1_WebChacheDeception/img/labCache_4.png)  

### 2.5
Копируем новый адрес в браузер и получаем значение API для carlos  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Lab_PortSwigger/Lab1_WebChacheDeception/img/labCache_5.png)  

### 2.6 
Результат выполнения лабораторной работы  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Lab_PortSwigger/Lab1_WebChacheDeception/img/labCache_6.png)  

