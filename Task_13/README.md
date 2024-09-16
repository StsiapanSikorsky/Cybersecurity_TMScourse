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
![image]()  

Для наделения правами администратора нажимаем ПКМ на созданного пользователя и выбираем Properties:  
![image]()  

В открывшемся окне переходим во вкладку Member Of, который выводит нам список групп пользователя, нажимаем Add:  
![image]()  

В открывшимся окне нажимаем Advanced:
![image]()  

Нажимаем **Find Now** и выбираем группы для присвоения пользователю, присваиваем Administrator:  
![image]()  

Теперь пользователь Sikorsky является администратором:  
![image]()  

- Запись пароля в хранилище

### 1.2 Создать УЗ без административных прав для сотрудника  
Создаем УЗ пользователя **"Ivanov"**, при этом оставляем включенным опцию "Требовать смены пароля при следующем входе в систему":    
![image]()  

Проверяем права нового пользователя, пользователь состоит только в группе User, без группы администратора:  
![image]()  

### 1.3 Отключить УЗ "Гость"  
Переходим по следующему пути:  
>ПКМ по Пуск->computer manage(управление компьютером)->local users(локальные пользователи)->users->Guest    

![image]()  

- Переходим по следующему пути:  
>Поиск->local security policy(локальная политика безопасности)->local policies(локальные политики)->security options(параметры безопасности)

В появившемся списке находим **Account: Guesst account status** и проверяем статус (должен находиться в disabled)  
![image]()  

### 1.4 Включение контроля учетных записей (UAC)  
Для включения UAC переходим по следующему пути:  
>Пуск->control panel(панель управления)->User Account(учетные записи пользователей)->User Account->Chnge User Account Control settings(Изменить параметры контроля учетных записей)  

Устанавливаем ползунок в положение "Уведомлять только при попытках приложений внести изменения в компьютер (по умолчанию)":  
![image]()  


### 1.5 Настройка парольной политики  
Для настройки парольной политики переходим по следующему пути:  
>Поиск->Local security policy->Account policy

Воткрывшемся окне редактируем **Password Police** и **Account Lockout Policy**
- вести журнал паролей - 5 последних паролей  
- максимальный срок действия паролей - 90 дней  
- минимальная длина пароля - 8 символов  
- пароль должен отвечать требованиям сложности - включено  
![image]()  

- пороговое значение блокировки - 5 ошибок  
- продолжительность блокировки УЗ - 15 мин  
![image]()
