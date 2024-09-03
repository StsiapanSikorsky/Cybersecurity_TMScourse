# Домашнее задание 8 - типы атак Ч2 (Spam, DDOS, botnet, MIM, Viruses)

**1) Провести DOS атаку на Juice Shop**  
- запустить container JuiceShop и произвести dos
- [XerXes - Most powerful dos tool bY mR.Thg](https://github.com/XCHADXFAQ77X/XERXES)
- Сделать скрин нагрузки на docker container вывод команды  >top

**2)Изучить типы и средства sppofing-a лекции**
- Придумать ссылки либо название средств с помощью которых можно осуществить спуффинг вида:  
_1_. Подмена номера;  
_2_. Подмена сайта;  
_3_. Подмена почты;  
_4_. IP spoofing;  
_5_. DNS spoofing;  
_6_. SMS spoofing;  
_7_. ARP spoofing;  
_8_. Extension spoofing.  

## 1) Провести DOS атаку на JuiceShop  
### 1.1 Запуск контэйнера Docker JuiceShop  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task8/img/Docker_StartJuiceShop.png)  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task8/img/JuiceShop_Window.png)  

### 1.2 Запуск DOS сервиса Xerxes  
- Скачивание репозитория с github  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task8/img/Xerxes_1_coppy.png)    

- Компиляция программы  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task8/img/Xerxes_2_compil.png)   

- Запуск Xerxes  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task8/img/Xerxes_3_startAttack.png)   

### 1.3 Нагрузка во время атаки  
- Результат нагрузки до атаки  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task8/img/CPU_beforeAttack.png)    

- Результат нагрузки во время атаки (CPU возросло на 10-20%)  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task8/img/CPU_afterAttack.png)

- Результаты до и во время атаки при помощи команды, а также вывод логов  
>docker stats >> logs

![image]()  
![image]()  
