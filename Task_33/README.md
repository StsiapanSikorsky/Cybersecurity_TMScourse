# Домашнее задание №33: Reverse engineering  
1) Ознакомиться с основными ресурсами Reverse engineering  
2) Проанализировать malware [crackme.exe](https://fatihhcelik.github.io/posts/The-First-CrackMe-of-The-Series-CrackMe1/)  
- скачать malware  
- скачать [process monitor hacker](https://processhacker.sourceforge.io/downloads.php)  
- скачать и посмотреть функционал [IDA](https://hex-rays.com/ida-free), [CFFExplorer](https://download.cnet.com/cff-explorer/3000-2383_4-10431156.html)  
- запустить monitor hacker, затем malware.exe  

Ссылки на дополнительные ресурсы:  
- [Active Directory Pentest Roadmap](https://orange-cyberdefense.github.io/ocd-mindmaps/img/pentest_ad_dark_2022_11.svg)  
- [Базы данных malware](https://bazaar.abuse.ch/browse/)  
- [crackme.exe](https://fatihhcelik.github.io/posts/The-First-CrackMe-of-The-Series-CrackMe1/)  
- [Process Hacker](https://processhacker.sourceforge.io/downloads.php)  


## 2) Анализ crackme.exe  
### 2.1 Скачать crackme.exe  
Скачивание с репозитория GitHub:  
![Crack_1]()  
Скаченный файл CrackMe1.exe  
![Crack_2]()  

### 2.2 Process monitor hacker  
- запуск process monitor hacker  
![ProcM_1]()  
Программа мониторит и анализирует все запущенные процессы на ОС Windows, работу Firewall и сети.  

### 2.3 IDA  
- Скачивание IDA Free
Для скачивания и получению ключа необходимо пройти регистрацию, после чего скачиваем IDA Free на выбранную ОС, также скачиваем лицензионный ключ и закидаваем еего в корневую папку с IDA  
![IDA_1]()  

Запускаем программу для файла CrackMe1.exe  
![IDA_2]()  

### 2.4 CFF Explorer  
CFF Explorer - инструмент позволяющий анализирвать испольняемые файлы и редактировать их  
![CFF_1]()  

