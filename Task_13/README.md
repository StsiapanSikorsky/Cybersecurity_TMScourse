# Домашнее задание 13: безопасноть ОС Windows
**1) Установить ВМ Windows server 2019**  
- выполнить все пункты настройки windows согласно пунктов 13 занятия, слайдов 22-29  

**2) Добавить роль контроллера домена Active Directory**  
- имя домена "фамилияя латиницей".local (пример:sikorsky.local)  
- имя Windows server ns1  

**3) Настроить службу DNS**  
- изменить имя windows server на ns1  
- поднять DNS на Windows server  
- добавить A записи DNS, в том числе и для VM ubuntu, metasploit, kali  
- осуществить dig вашего name servera, приложить отчет  
- осуществить ping запрос по доменному имени всех VM  

**Ссылки на дополнительные материалы**  
- [Как работает Windows](https://uchet-jkh.ru/i/kak-rabotaet-operacionnaya-sistema-windows-principy-i-funkcionalnost/)  
- [regedit.exe Реестр Windows](https://itspectr.ru/chto-takoe-reestr-windows-vvodnaya-chast/)  
- [Network protocol Kerberos](https://www.keepersecurity.com/ru_RU/resources/glossary/what-is-kerberos/)  
- [Audit Windows настройка для SOC](https://www.anti-malware.ru/practice/methods/Setting-up-auditing-in-Windows-for-full-SOC-monitoring)  
- [Групповые политики GPO Windows](https://1cloud.ru/help/windows/gruppovye-politiki-active-directory)  
- [GPO Windows server Best Practice](https://winitpro.ru/index.php/category/group-policy/)  
- [LAPS утилита для безопасности локальных паролей AD](https://activedirectorypro.com/microsoft-laps-setup-install-guide/)  

## 1) Установить ВМ Windows server 2019  
### 1.1 Создать УЗ с административными правами
Для создания нового пользователя в OС Windows Serwer 2019 необходимо перейти по следующему пути:  
>Пуск->Settings->Accounts->Other users->Add->Users  

Создаем профиль Sikorsky:
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1_CreateAdm1.png)  

Для наделения правами администратора нажимаем ПКМ на созданного пользователя и выбираем Properties:  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1_CreateAdm2.png)  

В открывшемся окне переходим во вкладку Member Of, который выводит нам список групп пользователя, нажимаем Add:  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1_CreateAdm3.png)  

В открывшимся окне нажимаем Advanced:  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1_CreateAdm4.png)  

Нажимаем **Find Now** и выбираем группы для присвоения пользователю, присваиваем Administrator:  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1_CreateAdm5.png)  

Теперь пользователь Sikorsky является администратором



### 1.2 Создать УЗ без административных прав для сотрудника  
Создаем УЗ пользователя **"Ivanov"**, при этом оставляем включенным опцию "Требовать смены пароля при следующем входе в систему":    
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1_CreateUser1.png)  

Проверяем права нового пользователя, пользователь состоит только в группе User, без группы администратора:  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1_CreateUser2.png)  

### 1.3 Отключить УЗ "Гость"  
Переходим по следующему пути:  
>ПКМ по Пуск->computer manage(управление компьютером)->local users(локальные пользователи)->users->Guest    

![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.3_CheckGuest.png)  

Переходим по следующему пути:  
>Поиск->local security policy(локальная политика безопасности)->local policies(локальные политики)->security options(параметры безопасности)

В появившемся списке находим **Account: Guesst account status** и проверяем статус (должен находиться в disabled)   
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.3_Guest2.png)  

### 1.4 Включение контроля учетных записей (UAC)  
Для включения UAC переходим по следующему пути:  
>Пуск->control panel(панель управления)->User Account(учетные записи пользователей)->User Account->Chnge User Account Control settings(Изменить параметры контроля учетных записей)  

Устанавливаем ползунок в положение "Уведомлять только при попытках приложений внести изменения в компьютер (по умолчанию)":  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.4_onUAC.png)  


### 1.5 Настройка парольной политики  
Для настройки парольной политики переходим по следующему пути:  
>Поиск->Local security policy->Account policy

Воткрывшемся окне редактируем **Password Police** и **Account Lockout Policy**
- вести журнал паролей - 5 последних паролей  
- максимальный срок действия паролей - 90 дней  
- минимальная длина пароля - 8 символов  
- пароль должен отвечать требованиям сложности - включено  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.5_PasswordPolitic1.png)  

- пороговое значение блокировки - 5 ошибок  
- продолжительность блокировки УЗ - 15 мин  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.5_PasswordPolitic2.png)  

### 1.6 Настройка парольной политики PIN (Windows Hello)  
Длянастройки парольной политики переходим по следующему пути:  
> cmd->gpedit.msc->Computer configeration->Administrative tempates(административные шаблоны)->System->PIN Complexity(сложность PIN-кода)  

>!IMORTANT  
gpedit.msc - вход в групповые политики устройства  

Выставляемые значения:
- требовать использование цифр - включено  
- требование использования строчных букв - включено  
- минимальная длин PIN-кода - 8 символов  
- срок действия - 90 дней  
- журнал - последних 5 паролей  
- требовать использование специальны символов - включено  
- требовать использование прописных букв - включено  
![1.6_PINPolicySettings](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.6_PINPoliceSettings.png)  


### 1.7 Включение RDP для УЗ администратора  
Для включения RDP для администратора в Winows10 переходим по следующему пути  
> Пуск->Settings->System->Remote Desktop(удаленый рабочий стол)->Enable Remote Desktop (On)  

![1.7_OnRDP](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.7_OnRDP.png)    

Добавлям пользователей, которые могут получить удаленный доступ (добавляем УЗ администраторов)  
![1.7_AddAdmin](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.7_AddAdmin.png)  

Заходим в дополнительные параметры и включаем "Требовать использование устройствами аутентификации на уровне сети для подключения"  
![1.7_OnAuthentication](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.7_OnAuthentication.png)  


### 1.8 Настройка блокировки абочего стола  
Для настройки блокировки рабочего стола переходим:  
>Поиск->Local Security Policy->Local Policy->Security Options  

Находим параметр "Интерактивный вход в систему:предел простоя компьютера" ("Interactive logon:Machine inactivity limit") и выставляем значение 300 секунд  
![1.8_InactivityLimit](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.8_InactivityLimit.png)  

### 1.9 Настройка установки обновлений  
Для настройки установки обновлений переходим:  
> Пуск->Settings->Update & Security->Windows update  

Производим выполнение обновлений для ВМ WindowsServer2019  
![1.9_Update](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.9_Update.png)  

Устанавливаем период активности компьютера в "change active hours"  
![1.9_SetActiveHours](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.9_SetActiveHours.png)  


### 1.10 Шифрование ЖД устройства с помощь BitLocker
Устройство не поддерживает возможность шифрования, что указано в сведениях о системе
![1.10_EncryptionNot](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.10_NotEncryption.png)  


### 1.11 Включение брандмауэра и настройка логирования  
Заходим в Windows Firewall и убеждаемся, что он включен  
![1.11_OnFirewall](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.11_OnFirewall.png)  

В "Windows Defender Firewall Properties" нажимаем ПКМ и переходим к настройке логгирования (Logging->Customize), где выставляем следующие настройки:  
- включить запись пропущенных пакетов  
- включить запись успешных подключений  
- размер файла лога - 10240КБ  

![1.11_SettingsOfLogging](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/1.11_SettingsOfLogging.png)


## 2) Добавить роль контроллера домена Active Directory
### 2.1 Установка Active Directory
В диспетчере серверов (Server Manage) во вкладке Панель мониторинга (Dashboard) кликаем на **"Добавить роли и компоненты" (Add roles and features wizzard)**   
![AD1_SetupStep1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD1_SetupStep1.png)  

Выбираем сервер, на который устанавливаем Active Directory  
![AD1_SetupStep2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD1_SetupStep2.png)  

Выбираем роль - Доменные службы Active Directory  
![AD1_SetupStep3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD1_SetupStep3.png)  

Процесс выполнения установки
![AD1_SetupStep4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD1_SetupStep4.png)   

### 2.2 Добавление домена и создание леса  
После успешной установки Диспетчер серверов просит нас повысить уровень привелегий сервера, для этого кликаем на флаг с восклицательным знаком    
![AD2_UpServer1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD2_UpServer1.png)   

После выбираем роль домену:  
- добавить доменный контроллер в существующий домен  
- добавить новый домен в лес  
- добавить новый лес  

Поскоольку это первый домен, выбираем добавить новый лес. Также выбираем доменное имя **"sikorsky.local"**  
![AD2_AddForest](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD2_AddForest.png)  

Задаем пароль резервной службе востановления каталогов DSNS  
![AD2_UpServer3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD2_UpServer3.png)  

По Best Practise меняем пути  
![AD2_UpServer4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD2_UpServer4.png)  

После перезагрузки, домен полностью установлен  
![AD2_UpServer5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD2_UpServer5.png)  

### 2.3 Групповые политики 
Для просмотра групповых политик леса переходим:  
> Tools->Groupe Policy Managment  

![AD3_Policy1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD3_Policy1.png)  

>[!NOTE]  
Все домены подключаемы к Active Directory будут наследовать и применять дефолтную олитику с данного раздела (менять ее не рекомендуется)  

Для добавления новой GPO (Групповойй политики), нажимаем ПКМ по доменному имени и выбираем первый пункт  
![AD3_Policy2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD3_Policy2.png)  

Как результат создается GPO (testGPO) применяемая ко всем контейнерам ниже  
![AD3_Policy3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD3_Policy3.png)    

### 2.4 Создание в доменном контроллере организационных юнитов  
Переходим  
>Tools->Active Directory Users And Computers  

Во вкладке "доменные контроллеры" создаем контейнер, объединяющий собой определенный отдел (в данном случае просто работники)  
![AD4_AddUnit1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD4_AddUnit1.png)  

Добавляем работников  
![AD4_AddUnit2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_13/img/AD4_AddUnit2.png)  

### 2.5 Добавление машины в домен  
Чтобы добавить машину в домен, предварительно в Active Directory создать пользователя.  

### 2.5.1 Настройка добавляемой машины  
На ВМ Windows10 настраиваем имя компьютера, а также добавляем домен  
- изменяем адрес предпочтительного DNS-сервера
- заходим в "Свойства" моего компьютера  

![2.5_SettingsWin10_0]()  

- в сопутствующих параметрах выбираем "Переименование этого ПК"  

![2.5_SettingsWin10_1]()  

- изменяем имя и добавляем домен   

![2.5_SettingsWin10_2]()  

- вводим данные, кто имеет право добавить в домен (в нашем случае Administrator)  

![2.5_SettingsWin10_3]()  

>[!WARNING]  
Best Practice: создать пользователя с правами на добавления машин в домен, чтобы администратор не светился в логах  

- как результат видим сообщение  

![2.5_SettingsWin10_4]() 



