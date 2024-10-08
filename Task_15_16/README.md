# Домашнее задание №15-16: Защита инфраструктуры предприятия  
1) Поднять контролер домена DC1 в отдельной подсеи  
- Установить роль DHCP сервера в AD, с раздачей настроек IP и DNS  
- Поднять VM Win10 в данной подсети, проверить получение сетевых настроек данной ВМ по DHCP  
- Добавить данную ВМ в домен <фамилия>.tms  

2) Настроить AD GPO согласно лучших практик  
- Создать контейнер - организационный юнит OU, в ней 2 контейнера OU fin и hr и по 2 пользователя в каждом контейнре  
- Для OU fin создать и прикрепить fin_gpo и настроить парольную политику сложности пароля 10 символов, 5 паролей не должно совпадать, срок действия пароля 90 дней  
- Для OU hr создать и прикрепить hr_gpo и настроить парольную политику сложности пароля 8 симвоов, 180 дней срок действия, блокировка экрана 15 минут после бездействия  
- Зайти под одним из данных пользователей на VM Win10, ввести в Powershell примененные групповые политики командой **gpresult /r**  

Ссылки на дополнительные ресурсы  
-[Групповые политики GPO Windows](https://1cloud.ru/help/windows/gruppovye-politiki-active-directory)  
-[Настройки политики паролей в домене AD](https://winitpro.ru/index.php/2018/10/26/politika-parolej-uchetnyx-zapisej-v-active-directory/)  
-[gpresult /r](https://winitpro.ru/index.php/2014/08/15/gpresult-diagnostika-primeneniya-gruppovyx-politik/)  
-[Dot1x настройка аутентификации](https://uwaterloo.atlassian.net/wiki/spaces/ISTKB/pages/361791643/Windows+10+802.1x+Wired+Authentication)  
-[LAPS утилита для безопасности локальных паролей AD](https://activedirectorypro.com/microsoft-laps-setup-install-guide/)  
-[Audit Windows настройка для SOC](https://www.anti-malware.ru/practice/methods/Setting-up-auditing-in-Windows-for-full-SOC-monitoring)  
-[Ubuntu as router with iptables and 2 interfaces firewall](https://medium.com/@lfoster49203/setting-up-ubuntu-as-a-router-with-advanced-routing-features-4511abc5e1eb)  

## 1) Поднять контроллер домена в отдельной подсети  
### 1.1 Установка DHCP сервера в AD с раздачей настроек IP и DNS  
Для назначения роли DHCP сервера домену AD переходим во вкладку **Manage** и выбираем **Add Roles and Features**   
![DHCP_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_1.png)

В открывшемся окне выбираем **DHCP Server**  
![DHCP_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_2.png)  

После установки DHCP сервера нажимаем на флажок и выбираем **Complete DHCP configuration**  
![DHCP_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_3.png)  

После установки DHCP сервера необходимо добавить пул адресов для раздачи, для этого во вкладке "Выполнить" (Win+R) вводим следующую команду:  
>dhcpmgmt.msc  

Как результат будет открыто окно управления настнойками DHCP сервера  
![DHCP_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_4.png)  

Для разворачивания DHCP сервера в IPv4 щелкаем на ПКМ и выбираем **New Scope...**  
![DHCP_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_5.png)  

В открывшемся окне указываем название DHCP области  
![DHCP_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_6.png)  

Указываем пул адресов, а также маску посети  
![DHCP_7](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_7.png)  

В следующем окне указываются запрещенные адреса для раздачи (установлены небыли). 
Далее указываем длительность аренды IP адреса (по умолчанию оставляем 8 дней)  
![DHCP_8](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_8.png)  

Указываем IP адрес шлюза клиентам  
![DHCP_9](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_9.png)  

Указываем имя домена и адреса DHCP серверов (оставляем по уммолчанию)  
![DHCP_10](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_10.png)  

### 1.2 Проверка получения DHCP адреса на ВМ Win10  
Для получения IP адреса по DHCP в настройках сетевого адаптера отключаем статический адрес IPv4 и ставим получение адреса по DHCP.  
Проверяем в консоли IPv4 машины, а также пинг с DHCP сервером  
![DHCP_11](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/DHCP_11.png)  

### 1.3 Добавление в домен  
Ранее в **Task 13** ВМ Win10 была добавлена в домен **sicorsky.local**  


## 2) Настройка AD GPO согласно лучших пактик  
### 2.1 Создание контейнеров OU и их пользователей  
Для создания контейнеров OU переходим в:
>Tools->Active Directory Users and Computers 

В открывшемся окне во вкладке переходим во вкладку доменные контроллеры и создаем два контейнера: fin и hr  
![GPO_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/GPO_1.png)  

Добавляем по два пользователя (Fin1, Fin2, hr1, hr2) в соответствующие контейнеры  
![GPO_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/GPO_2.png)  

### 2.2 Создание fin_gpo  
Для создания групповой политики fin_gpo переходим:
>Tools->Group Policy Managment

В открывшемся окне выбираем **Domain controllers**, нажимаем ПКМ по вкладке fin и выбираем **"Create GPO in this domain"** с именем **fin_gpo**  
![GPO_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/GPO_3.png)  

После создания политики кликаем по ней ПКМ и выбираем **Edit**   
![GPO_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/GPO_4.png)  

В открывшемся окне переходим:
>Computer Configuration->Policies->Windows Settings->Security Settings->Account Policies->Password Policy  

Ставим заданные значения парольной политики для организационных юнитов fin   
![GPO_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/GPO_5.png)  

### 2.3 Создание hr_gpo  
Повторяем действия перечисленные в пункте выше, ставя соответствующие параметры  
![GPO_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/GPO_6.png)  

Настройка блокировки экрана происходит в **Account Lockout Policy**   
![GPO_7](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/GPO_7.png)   


### 2.4 Проверка применения GPO на ВМ Win10   
Вход в систему Win10 осуществляем под пользователем Fin1  
![GoWin10_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/GoWin10_1.png)   

Проверка примененных групповых политик командой gpresult /r  
![GoWin10_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_15_16/img/GoWin10_2.png)  







