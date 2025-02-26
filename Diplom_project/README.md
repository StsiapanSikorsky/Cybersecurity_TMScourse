# Дипломный проект:
## 1. Расследование инцидентов (ответы на вопросы)  

### 1) У Вас есть логи безопасности для фаервола между DMZ и интернетом. Как вы будете использовать эти логи для обнаружения угроз?  
**Ответ:**  
Логи фаервола содержат информацию о входящем и исходящем трафике, что позволяет выявить подозрительные активности и потенциальные атаки. При помощи данных логов можно произвести следующие действия:    
- регулярный анализ логов на предмет аномальных паттернов (необычные объемы трафика, частые попытки входа или обращения к закрытым портам)    
- поиск и анализ IP-адресов, генерирующих большое количество запросов за короткий промежуток времени (DDoS, Brute force)  
- сравнение логов с БД известных вредоносных IP-адресов и доменов  
- проверка срабатывания правил firewall для выявления блокируемых соединений  
- использование системы обнаружения вторжений (IDS) для автоматического анализа логов и выявления подозрительных действий  
- на основе анализа логов и инцидентов обновление правил firewall для блокировки новых угроз и минимизации уязвимостей в системе  

### 2) Вы аналитик SOC и у Вас есть предупреждение от системы IDS о SQL-инъекции на Веб-сервер. Что вы будете делать? Как вы будете исследовать технические аспекты?  
**Ответ:**    
Последовательность действий:  
- изучение деталей системы IDS (время инцидента, IP-адрес, тип запросы, целевой URL)  
- изоляция инцидента, по возможности отключение  
- сбор логов и анализ реализованной злоумышленником SQL-инъекции  
- определение какие части уязвимы к SQL-инъекциям  
- воспроизвести атаку при помощи Burp Suite и понять ее последствия  
- внедрение мер по защите от SQL-инъекций  

### 3) Наиболее частые компромитирующие сценарии Windows связаны с использованием инструментов снимающих дамп хэшированного пароля. Предложите сценарии обнаружения (чем больше, тем лучше), использования инструментов хэш-дампов. Как обнаружить использование украденных полномочий?
**Ответ:**  
Для обнаружения несанкционированного доступа при помощи хэш-дампов следует:  
- проверить журналы событий Windows **(Win+R -> eventvwr.msc)** на наличие аномальных действий (несанкционированные входы, попытки доступа к системным файлам)  
- обратить внимание на события ID4624 (успешный вход) и ID4625 (неуспешный вход)  
- для предотвращения следует настроить аудит командной строки  
- для обнаружения следим за аномальными паттернами входа (нерабочее время или необычные местоположения)  
- для выявления активных пользователей на сервере испольуем коману **query user** 
- если имеется SIEM система анализируем ее логи  
- при возможности для предотвращения следует внедрить MFA (многофакторную аутентификацию)  
- при помои PowerShell отслеживаем запуск подозрительных процессов (mimikatz и hashcat)
```powershell
Get-Process | Where-Object { $_.Name -match "mimikatz|hashcat" }
```

### 4) Вы работаете в компании и имеете два офиса (Минск и Могилев), вы также имеете логи для VPN, Gateway, FireWall, системы управления физическим контролем доступа. Предложите сценарии для обнаружения возможных угроз.  
**Ответ:**  
Сценарии обнаржения возможных угроз:  
- анализ логов VPN (необычные IP-адреса, частота подключений, время подключения, сессии с высокой активностью)  
- мониторинг логов Gateway (аномальные HTTP-запросы, SQL-инъекции)  
- анализ логов Firewall (изучение блокировок трафика, повторяющиеся попытки доступа к защищенным ресурсам, использование необычных портов)  
- регулярный анализ логов и поиск в них скрытых угроз  
- интеграция SIEM системы, для корреляции событий из разных источников

### 5) Если у Вас есть антивирусные логи, какие правила корреляции (сценарии обнаружения) вы можете предложить?
**Ответ:**  
Сценарии обнаружения для антивирусных логов:  
- обнаружение массовых срабатываний антивируса  
- события о неудачных попытках удаления угроз  
- запуск подозрительных процессов (если процесс ранее не был замечен и пытается получить доступ к сетевым ресурсам или системны файлам)  
- паралельное срабатывание на разных устройствах  
- аномальные поведения учетных записей (если учетная запись иницирует доступ к критически важным объектам и системам)   
- повторяющиеся предупреждения об одной и тойже угрозе  
- корреляция с другими источниками логов  

### 6) Вы получили оповещение от корпоротивого прокси о том, что одна рабочая станция подключилась к вредоносномуу сату:  
#### 6.1 Какие немедленные действия предпринять для сдерживания распространения  
**Ответ:**   
- отключение зараженной станции от сети, для предотвращения распространения ВПО  
- проверка других систем на данное ВПО  
#### 6.2 В какой системе ожно попробовать получить дополнительную информацию  
**Ответ:**  
Получить дополнительную информацию ожно:
- в SIEM системе  
- анализ логов WAF  
#### 6.3 На каком этапе атаки "цпочки уничтожения" находится данный случай  
**Ответ:**   
Данный случай предположительно находится на этапе равертывания ВПО, так как скорее всего злоумышленник уже получил доступ к системе   

### 7) Из какой системы данный лог и что можно о нем сказать  
![1_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/1_4.png)  
**Ответ:**  
Логи из системы WAF, в нем можно найти информацию о том, когда был зафиксирован запрос, типы пакетов, уникальные идентификаторы пакетов, используемый протокол (UDP), вид запроса (Snd-исходящий), IP-источника запросов и используемый порт, запрашиваемое доменное имя.   
Поскольку большое количество запросов выполнялось в одно и тоже время, предположительно логи описывают DDoS атаку.  

### 8) Что происходит согласно следующим событиям  
![1_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/1_1.png)  
![1_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/1_2.png)  

### 9) Что означает сообщение? Оно подозрительное? Почему?  
![1_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/1_3.png)  
**Ответ:**   
Сообщение о запуске PSEXESVC.exe, позволяющего запускать администраторам процессы на удаленных системах и получатть вывод консольных приложений на локальной машине что является подозрительным, особенно если запущен на пользовательском ПК.  

### 10) Что можно сказать о данных логах  
![1_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/1_5.png)  
![1_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/1_6.png)  
![1_7](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/1_7.png)  
**Ответ:**  
Лог показывает загрузку и запуск вредоносного скрипта на PowerShell  

### 11) Что можно сказать о скрипте  
![1_8](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/1_8.png)  
**Ответ:**  
Действияя скрипта описаны в ДЗ №27 Ч2  

### 12) Какой идентификатор события имеет изменение реестра? Какой идентификатор события устанавливает службу и сообщает о сбоях службы?  
**Ответ:**  
ID4657 - идентификатор события для изменения реестра Windows  
ID7045 - идентификатор события для установки службы (событие фиксирует когда служба была установлена)  
ID7031 и ID7034 - идентификаторы события сбоя службы (фиксируют когда служба неожиденно завершает работу или аварийно останавливается)  

### 13) Почему файлы с расширением "chm" могут быть опасны?  
**Ответ:**   
- файлы .chm могут содержать HTML страницы которые включают в себя вредоносные скрипты на JavaScript  
- при открытии .chm файлов встроенный просмоторщик может не выдавать предупреждений о потенциально опасных действиях  
- легкость создания ВПО через .chm фалы  

### 14) У вас есть журналы DNS-сервера и вы видете множество запросов AXFR с оного внешнего IP-адреса. Это злонамеренные запросы? Если да, то почему?  
**Ответ:**   
AXFR-запросы предназначены для передачи зоны DNS между серверами и если настройка DNS-серверов неправильно сконфигурирована, то сервер можт отвечать на такие запросы из любого источника, что позволяет злоумышленнику получить полную информацию о домене и раскрыть внутреннюю инфроструктуру сети.  

### 15) Как обнаружить атаку Golden Ticket?  
**Ответ:**  
Атака Golden Ticket позволяе злоумышленнику получить возможность создания поддельных Kerberos билетов. Осноновные направления для обнаружения атаки:  
- мониторинг событий Kerberos (в нормальных условиях пользователь сначала запрашивает TGT, а затем использует его для получения TGS. При атаке злоумышленник минует этап запроса TGT)  
- анаиз логов с ID4769 - запрос TGS  
- анализ SIEM системы и анализ поведения пользователей, выявление отклонений от нормального поведения  

### 16) Представьте, что злоумышленник сломал ваш контроллер домена. предложите сценарии восстановления для данной ситуации.  
Контроллер домена - сервер управляющий доступом к ресурсам сети, аутентифиации пользователей и соблюдения политик безопасности в домене.  
**Ответ:**  
- изоляция контроллера домена (отключение от сети)  
- оценка ущерба (анализ логов, поиск скомпрометированной информации)  
- проверка целостности данных  
- восстановление контроллера домена из резервной копии  
- устранение уязвимости (изменение пароля всех учетных записей)  

### 17) Какая функция PowerShell_5 лучше всего подходит для службы безопасности  
**Ответ:**   
Для службы безопасности лучше всего подходит фаункция AMSI (Antimalware Scan Interface) позволяюая:  
- проводить проверки на ВПО (позволяет приожениям передавать данные о скриптах и командах в антивирус)  
- интеграция с защитой Windows (все блоки скриптов передаются в AMSI)  
- вызов методов .NET, что улучшает возможность обнаружения и предотвращеия атак  

### 18) Вы получили предупреждение от службы EDR и имеете только такую информацию:  
>Process: flashhelperservice.exe  
PID: 6508  
OS Type: windows   
MD5: 59c34bc243eb2604533b5f08d30944f8  
SHA-256: ef214626923d76e24ae5299dd16c53b15847e91a97d2eea79ce951c6bead9b7c     

**Ответ:**   
Алерт получен IDR системой. Процесс flashhelperservice.exe имеет низкий рейтинг безопасности, способен записывать ввод с клавиатуры и мыши, следовательно моет использоваться шпионским ВПО. Анализируя хэш файла на virustotal, было получено 25 предупреждений, что свидетельствует о вредоносе файла.    

### 19) В ходе расследования увидили информацию представленную ниже, что скрыто в этом коде?  
>JgBjAGgAYwBwAC4AYwBvAG0AIAA2ADUAMAAwADEAIAA+ACAAJABuAHUAbABsAAoAJABlAHgAZQBjAF8AdwByAGEAcABwAGUAcgBfAHMAdAByACAAPQAgACQAaQBuAHAAdQB0ACAAfAAgAE8AdQB0AC0AUwB0AHIAaQBuAGcACgAkAHMAcABsAGkAdABfAHAAYQByAHQAcwAgAD0AIAAkAGUAeABlAGMAXwB3AHIAYQBwAHAAZQByAF8AcwB0AHIALgBTAHAAbABpAHQAKABAACgAIgBgADAAYAAwAGAAMABgADAAIgApACwAIAAyACwAIABbAFMAdAByAGkAbgBnAFMAcABsAGkAdABPAHAAdABpAG8AbgBzAF0AOgA6AFIAZQBtAG8AdgBlAEUAbQBwAHQAeQBFAG4AdAByAGkAZQBzACkACgBJAGYAIAAoAC0AbgBvAHQAIAAkAHMAcABsAGkAdABfAHAAYQByAHQAcwAuAEwAZQBuAGcAdABoACAALQBlAHEAIAAyACkAIAB7ACAAdABoAHIAbwB3ACAAIgBpAG4AdgBhAGwAaQBkACAAcABhAHkAbABvAGEAZAAiACAAfQAKAFMAZQB0AC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAagBzAG8AbgBfAHIAYQB3ACAALQBWAGEAbAB1AGUAIAAkAHMAcABsAGkAdABfAHAAYQByAHQAcwBbADEAXQAKACQAZQB4AGUAYwBfAHcAcgBhAHAAcABlAHIAIAA9ACAAWwBTAGMAcgBpAHAAdABCAGwAbwBjAGsAXQA6ADoAQwByAGUAYQB0AGUAKAAkA
HMAcABsAGkAdABfAHAAYQByAHQAcwBbADAAXQApAAoAJgAkAGUAeABlAGMAXwB3AHIAYQBwAHAAZQByAA=  

Результат декодирования base64:
```PowerShell
&chcp.com 65001 > $null
$exec_wrapper_str = $input | Out-String
$split_parts = $exec_wrapper_str.Split(@("`0`0`0`0"), 2, [StringSplitOptions]::RemoveEmptyEntries)
If (-not $split_parts.Length -eq 2) { throw "invalid payload" }
Set-Variable -Name json_raw -Value $split_parts[1]
$exec_wrapper = [ScriptBlock]::Create($split_parts[0])
&$exec_wrapper
```  
**Ответ:**   
Код устанавливает кодировку UTF-8, получает входные данные и обрабатывет их как текст, после чего строка разделяется на часть и сохранятеся в массив, после чего производится сохранение данных в json формате. Последние команды создают скрипт PowerShell из введенного массива.   
Код потенциально опасен так как позволяет созадавать блоки скриптов для выполнения произвольного кода.  

### 20) Вы заметили предупреждение от EDR указанное ниже, нормально ли это и если нет, по какой причине?  
>c:\windows\system32\services.exe запускается explorer.exe  
**Ответ:**   
Запуск процесса explorer.exe чеерез services.exe может указывать на вредоносную активность, например злоумышленник мможет использовать имя services.exe для маскировки своих ВПО. Для защиты следует проверить расположение файла, он должен находится в каталоге **C:\Windows\System32**  

### 21) Вы установили приложение на свой ПК и оно не может подключиться к интернету. Антивирусные предупреждения отсутствуют и вы можете пользоваться интернетом. Какаова наиболее вероятная причина проблемы?  
**Ответ:**   
Вероятные причины:  
- разрешения приложения для доступа к сети  
- блокирование брандмауэром  
- блокирование антивирусом определенного сетевого трафика  

### 22) Что можно сказать о данном URL  
>www.iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com  

**Ответ:**   
Анализ URL через Virustotal показал небезопасность данного URL. Поиск и анализ информации о домене показал, что домен использовался для атаки ВПО-вымагателя используя протокол SMB для распространения и шифрования зараженных файлов.  

### 23) Что можно сказать об отчете о сканировании nmap, ессть ли какие либо проблемы безопасности?  
![1_9](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/1_9.png)  
**Ответ:**   
Отчет показал используемный открытый порт для SSH 22 (рекомендуется менять на кастомный) и используемые ключи хоста, а также какие приложения используют 80 порт tcp (Веб сервер Apache Tomcat c HTTP-коннектером Coyote)  


### 24) Восстановить пароль из хэша    
> fmarket.stf\admin:1337:aad3b435b51404eeaad3b435b51404ee:bebaecb23aa18f5375628541ff3fb3b8:::  

**Ответ:**    
Для определения типа хэша и определения параметров брутфорса был использован **perplexity** который показал, что хэш используется для хранения паролей Windows и состроит из двух частей: NTLM:MD4  
Была выбрана программа hascat со следующими параметрами:  
```
hashcat -m 1000 -a 3 hash2.txt ?а?а?а?а?а?а?а?а?а?а?а?а --increment --increment-min 4 --increment-max 12  
```  
>-m 1000 алгоритм хэширования NTLM  
-a 3 брутфорс  
?а?а?а?а?а?а?а?а?а?а?а?а маска букв большого и маленького регистра + цифры    
-increment-min 4 --increment-max 12 брутфорс от 4 до 12 символов  

### **Итоговый пароль: a6_123**  
![1_10](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/1_10.png)  


## 2. Создать скрипт который устанавиливает инструменты и снимает дамп оперативной памяти предоставляя его просмотр  
Код скрипта:  
```bash
#!/bin/bash

RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[0;33m'
CYAN='\033[0;36m'
RESET='\033[0m'

sudo apt update

#Install volatility
install_volatility() {
	if command -v volatility >dev/null 2>&1; then
		print -e "$GREEN Volatility is installed $RESET"
	else	
		echo -e "$YELLOW Install volatility $RESET"
		sudo git clone https://github.com/volatilityfoundation/volatility3.git
		cd volatility3
	fi	
	
	sudo python3 -m venv venv
	sudo source venv/bin/active
	sudo pip3 install -r requirements.txt
	echo -e "$GREEN Volatility has been installed $RESET"
}

#Install avml
install_avml(){
	echo -e "$YELLOW Install avml $RESET"
	cd ~
	sudo apt install curl wget
	sudo wget https://github.com/microsoft/avml/releases/download/v0.14.0/avml
	sudo chmod +x avml
	sudo mv avml /usr/local/bin
	echo -e "$GREEN avml has been installed $RESET"
}

#Install dwarf2json
install_dwaf2json(){
	echo -e "$YELLOW Install dwarf2json $RESET"
	sudo apt install dwarf2json
	git clone https://github.com/volatilityfoundation/dwarf2json
	cd dwarf2json
	sudo apt install golang-go
	go-build
	KERNEL=uname -r
	./dwarf2json linux --elf /boot/$KERNEL symboltable.json
	cd ~
	echo -e "$GREEN dwarf2json has been installed and sympol table has been create"
}

#Get dump
get_dump_avml(){
	echo -e "$YELLOW Get dump dump.dmp $RESET"
	sudo avml -o dump.dmp
	echo -e "$GREEN memory dump create $RESET"
}

#Search dump
search_dump(){
	echo -e "$YELLOW Search dump $RESET"
	uname -a
	cd volatility3
	sudo python3 vol.py -f ~/dump.dmp a 
}

install_volatility
install_avml
get_dump_avml
search_dump
```  
Результат выполнения скрипта:  
![2_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/2_1.png)  

## 3. Автоматизировать процесс проверки url через virustotal  

Для автоматизации процесса проверки URL через virustotal необходимо пройти регистрацию на их сайте, а также воспользоваться встроенным API, который находится в нашем профиле (переменная в  коде: apikey).

### Код скрипта  

```python
#!/usr/bin/env python3
import requests
import json

input_url = str(input("Сканирование, введите URL который хотите просканировать \n"))

#Отправка HTTP POST запроса
api_url = "https://www.virustotal.com/vtapi/v2/url/scan"
params = dict (apikey = "6322a317fe297cf1b310189b2bf1261df2afd557181e8f6ffa66963f75b72bb2", url = input_url)
response = requests.post(api_url, data = params)

#Обработка ответа
if response.status_code == 200:
#преобразование объекта json в словарь python
    result = response.json()
    #print(json.dumps(result, sort_keys = False, indent = 4))
else:
    print("Ошибка", response.status_code)

#Получение id отчета из словаря python
report_id = result.get('scan_id')

#Получение отчета о сканировании по id
print("Отчет о сканированном URL:")
api_url = 'https://www.virustotal.com/vtapi/v2/url/report'
params = dict(apikey='6322a317fe297cf1b310189b2bf1261df2afd557181e8f6ffa66963f75b72bb2', resource = report_id)
response = requests.get(api_url, params = params)
if response.status_code == 200:
  result=response.json()
  #print(json.dumps(result, sort_keys = False, indent = 4))

#Обработка результата
false_count = 0
true_count = 0
for key in result['scans']:
    result_detection = str(result['scans'][key]['detected'])
    if result_detection == 'False':
        false_count += 1
    else:
        true_count += 1
        print('Обнаружено в антивирусе: ',key)


print('Опасность обнаружена в ', true_count,'антивирусах')
print(false_count,' антивирусов показали что URL безопасен')
```

### Результат работы скрипта  
![Virustotal_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/Virustotal_1.png)

Результат работы скрипта, полностью соответствует результатам на проверки URL на сайте  
![Virustotal_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/Virustotal_2.png)    



## 4. Вы обнаруили уязвимость CVE-2021-41773 на вашем web сервере  
- вам необходимо создать задачу для IT по ее устранению  
- что нужно будет сделать специалисту, чтобы исправить эту уязвимость? Написать playbook для специалиста SOC L1.  

**CVE-2021-41773** - критическая уязвимость в Apache HTTP Server 2.4.49/50 которая характерезуется как уязвимость удаленного эксплоита кода. Дает возможность несанкционированного доступа к файлам за пределами установленного корневого каталога   

### Задача специалистам по устранению уязвимости  
1) Обновить Apache HTTP Server до версий 2.4.51 или более поздней  
2) Использовать защитную директиву **"Require all denied"** для ограничения доступа к ресурсам сервера (доступ осуществлять толлько по указанным разрешающим условиям доступа определенных пользователей или IP-адресов)  
3) Проверка web сервера на наличие использования уязвимости ранее, анализ логов  
4) Проверка устранения уязвимости при помощи использования специальной команды:  
```bash  
curl --silent --path-as-is --insecure "http://<АДРЕС СЕРВЕРА>/cgi-bin/.%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd" | grep -q "root.*" && echo "Host is vulnerable" || echo "Host is Not vulnerable"
```  

### Playbook
![Руководство по созданию Playbook (сценарий реагирования)](https://www.youtube.com/watch?v=jomLRu4UAjs&t=1s)   

![4_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/4_1.png)  
