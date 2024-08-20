# Домашнее задание 5 - Сети, маршрутизация Ч.2

1) **Изучение конфигурации роутера**
- Зайти в настройки домашнего роутера;
- Изучение настроек, скриншоты проброса портов приложений.
2) **Работа с Cisko Packet Tracer**
- Установка Cisco Packet Tracer;
- Сборка базовой схемы комп-свитч-роутер-свитч-комп
- Сегминтирование сети на 10 и 20 vlan, видимость хостов;
- Настройка сети, echo ping запросы между хостами;
- Слежение на симуляции за пакетами ICMP.

## 1) Изучение конфигурации роутера
### 1.1 Зайти в настройки домашнего роутера
- Домашний роутер: TP_Link Archer64  
Вход осуществлялся по IPv4 192.168.0.1  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgTP_Link/Router_TP_Link_Archer%20A64.png)  

### 1.1 Изучение настроек
- Пул адресов предоставляемый модемом  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgTP_Link/TPL_DHCP.png)  

- Список подключенных DHCP устройств  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgTP_Link/TPL_DHCP_settings.png)  

- Список подключенных устройств 
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgTP_Link/TPL_connect._Device.png)  

- Включение технологии NAT  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgTP_Link/TPL_OpenNAT.png)  

- Добавление перенаправления портов NAT  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgTP_Link/NAT_pereadres.png)  

### 1.2 Проброс портов
Проброс портов - технология позволяющая обращаться из Интернета к компьютеру, во внутренней сети за маршрутизатором, использующим технологию NAT.  
 Доступ осуществляется при помощи перенаправления трафика определенных портов с внешнего адреса маршрутизатора на адрес выбранного компьютера в локальной сети.

 #### Для осуществления данной функцции необходимо:
 1) В меню настроек роутера перейти на DHCP-сервис и зарезервировать адрес для определенного устройства (записываем MAC адрес устройства для которого выполняем проброс и задаем ему статический IPv4 LAN сети) 
 ![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgTP_Link/Probr1.png)  

 2) Перходим во вкладку NAT-переадресация->Перенаправление задаем виртуальный сервис, который мы хотим добавить  
 ![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgTP_Link/Probr2.png)  

 3) После изменений производим сохранение






## 2) Работа с Cisko Packet Tracer
### 2.1 Установка Cisko Packet tracer  
- Для установки требуется включить VPN сервис (была подключена локация Великобритании). Скаченная версия 8.2.2  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgCiskoPacket/Setup_CiskoPacketTracer%20v8.2.2.png)  

- Первичной настройкой для удобство пользования была включена настройка отображения портов (Ctr+R)  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgCiskoPacket/SetupShowPorts.png) 

- Установлены статические IPv4 адреса на добавленные компьютеры  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgCiskoPacket/Config_PC.png)   

> PC0 192.168.10.6/24  (VLAN-10)  
PC1 192.168.10.2/24  (VLAN-10)  
PC2 192.168.10.3/24  (VLAN-10)  
PC3 192.168.20.6/24  (VLAN-20)  
PC4 192.168.20.2/24  (VLAN-20)  
PC5 192.168.20.10/24  (VLAN-10)  
PC6 192.168.10.5/24  (VLAN-10)  
PC7 192.168.20.4/24  (VLAN-20)    
PC8 192.168.20.5/24  (VLAN-20)  
PC9 192.168.20.3/24 (VLAN-20)  

- После установки адресов, была проведена проверка, через консоль, на примере машины PC0 (в дальнейшем адрес был изменен на 192.168.10.6, так как 192.168.10.1 был присвоен шлюзу маршрутизатора)  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgCiskoPacket/ipconfig_PC.png)

### 1.2 Cборка базовой схемы
- Базовая схема представляет собой две подсети соединенные между собой маршрутизатором. Подсети разделены по принципу:  
Устройства в адрес которых включено значение "20" в третьем разряде, не должны контактировать с компьютерами со значением "10". 

> [!WARNING]  
За исключением PC0-2 из первой подсети, должны контактировать с устройством PC5 из второй подсети. (Данное условие было поставлено для отработки обмена пакетами через маршрутизатор)

- Схема построенной сети приведена на скриншоте
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgCiskoPacket/Simulation_Work.png)

### 1.3 Настройка сети на 10 и 20 vlan, видимость хостов
- Для настройки VLAN следует перечень VLAN добавить в коммутатор  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgCiskoPacket/add_vlan_switch.png)  

- В дальнейшем каждому порту присваивается определенный VLAN по принципу: к портам подводимым к устройству с адресом "10" в третьем разряде VLAN10, с адресом "20" - VLAN20  

>[!WARNING]  
За исключением устройства PC5 во второй подсети, данное устройство имеет адрес 192.168.20.10/24 и VLAN-10, для обеспечения обмена информации между заданными ранее устройствами  

![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgCiskoPacket/Setup_VLAN_Switch.png)

### 1.4 Настройка сети, echo-ping запросы между хостами
- Поскольку сеть была настроена ранее, осталось провести лишь пинг запросы между взаимодействующими хостами  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgCiskoPacket/Correct_network1.png)


### 1.5 Слежение на симуляции за пакетами ICMP
- При проведении работы, отслеживание для понимания работы осуществлялось на каждом этапе, на рисунке изображен пример промежуточного маршрута ping-запроса от PC2 (192.168.10.3) к PC5 (192.168.20.10) через маршрутизатор  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task5/imgCiskoPacket/Simulation_Work.png)  

>[!WARNING]  
Настройка маршрутизатора:  
Порт №1 - 192.168.10.1  
Порт №2 - 192.168.20.1
PC5 имеет шлюз номер порта №2 маршрутизатора, PC0-2 - номер порта №1 маршрутизатора


