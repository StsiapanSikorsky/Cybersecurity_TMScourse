# Домашнее задание 14: Безопасность ОС Linux  
1) Настроить ВМ Kali linux  
- BIOS/UEFI + парольную политику (слайд 26-30) 
- настроить iptables правила в виде файла скрипта *.sh (скрипт приложить в папку с ДЗ)   
    - разрешить все соединения по 80 и 443 порту
    - разрешить подключение к 22 порту только из внутренней сети  
    - натировать (nat) весь трафик через интерфейс ВМ  
- очистить все правила iptables, установить UFW firewall  
    - повторить все правила для iptables  

**Ссылки на дополнительные ресурсы**  
- [UEFI vs BIOS What the Difference](https://www.freecodecamp.org/news/uefi-vs-bios/)  
- [Что такое ядро Linux](https://losst.pro/chto-takoe-yadro-linux)  
- [Модули ядра Linux](https://losst.pro/moduli-yadra-linux)  
- [6 Уровней загрузки ОС](https://habr.com/ru/articles/113350/)  
- [SELinux](https://losst.pro/nastrojka-selinux)  
- [IPtables и примеры](https://habr.com/ru/articles/747616/)  
- [UFM firewall examples](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)  
- [SELinux vs AppArmor](https://www.techtarget.com/searchdatacenter/tip/Compare-two-Linux-security-modules-SELinux-vs-AppArmor)  
- [Ubuntu 20.04 64-bit PC server install](https://releases.ubuntu.com/20.04.6/ubuntu-20.04.6-live-server-amd64.iso)  


## 1.1 Настройка UEFI и парольной политики  
### 1.1.1 Настройка UEFI  
- Установка пароля в UEFI (ASUS Tuf Gaming F15)  
![UEFI_1]()  

- Проверка запроса пароля после перезагрузки UEFI  
![UEFI_2]()  

- Установка опции SecureBoot и отключение всех лишних вариантов загрузки  
![UEFI_3]()  

- Запрет на использование флешь-накопителей  
![UEFI_4]()  

- Проверка работы чипа TPM  
    - В строке "Выполнить" задаем команду  
> tpm.msc  

    - Переходим в окно настроек чипа TPM  
![TPM_1]()  

    - Проверяем версию чипа, в нашем случае v2.0 

### 1.1.2 Изменение имени устройства в Kali Linux  
- Для изменения имени устройства в Kali Linux необходимо отредактировать файл /etc/hostname, для этого используем команду  
>hostname sethostname itminsk230198  

![hostname_1]()

Также необходимо для избежания ошибок отредактировать файл /etc/hosts  
![hostname_2]() 

- Для изменения имени root необходимо заменить название root в двух файлах  
> /etc/passwd

![root_1]()  

> /etc/shadow  

![root_2]()  

### 1.1.3 Настройка парольной политики  
- Устанавливаем модуль Crack PAM  
> sudo apt-get install libpam-cracklib  

- Открываем файл конфигурации   
> sudo vim /etc/pam.d/common-password

- В открывшимся файле в pam_cracklib.so устанавливаем максимальную длину пароля **minlen=10**  

- В pam_cracklib.so устанавливаем сложность пароля  
>ucredit=-1 (минимум одна заглавная буква)  
lcredit=-1 (минимум одна строчная буква)  
dcredit=-1 
ocredit=-1  

![passwd_1]()  

- Установка даты истечения пароля 
>sudo vim /etc/login.defs  

![passwd_2]()  

## 1.2 Настройка iptables  
- разрешить все соединения по 80 и 443 порту  
- разрешить подключение к 22 порту только из внутренней сети  
Скриншот скрипта:  
![iptables_1]()  
Результат работы скрипта:  
![iptables_2]()  

### 1.3 Очистка правил iptables и установка UFM firewall
- Для очистки **всех** правил iptables используем следующую команду  
>iptables -F  

- Установка, включение и доггирование UFW firewall:  
>sudo apt install ufw
sudo ufw enable  
sudo ufw logging high

- Задаем правила для UFW firewall  
>sudo ufw allow from 10.10.0.0/24  
sudo ufw allow OpenSSH  
sudo ufw allow from 10.10.0.0/24 proto tcp to any port 22    
sudo ufw allow http  
sudo ufw allow proto tcp from any to any port 80,443  

![ufw_1]()  

- После добавления правил в UFW firewall перезагружаем службу  
>sudo ufw reload  

- Проверяем правила добавленные в UFW firewall  
>sudo ufw status verbose  

![ufw_2]()  

- Проверяем правила для iptables после настройки UFW firewall и убеждаемся в применении данных правил   
![iptablesAfterUfw]()  







