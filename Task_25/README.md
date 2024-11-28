# Домашнее задание №25: Forensics, Incident response  

1) Изучить основные виды HTTP methods and requests  
2) Установка volatility  
- установить набор програмных инструментов для криминалистического анализа данных [Volatility](https://github.com/volatilityfoundation/volatility3)  
3) Установить avml либо Lime  
- снять дамп ram (оперативной памяти) linux с помощью [AVML](https://github.com/microsoft/avml)  
- узнать точно профиль вашей линукс системы (uname -a)  
- с помощью набора инстументив [Volatility передав точный imageinfo](https://docs.google.com/document/d/1v7u6HVrae1R4fCCs1SNAGryjy5tmJCPDKq2Hyhqd9Fo/edit?usp=sharing) (профиль из которого сняли дамп) открыть дамп оперативной памяти, прикрепить скрин вывода  

Ссылки на дополнительные ресурсы:  
- [HTTP methods, headers, responses](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)  
- [ELK подробный обзор](https://www.youtube.com/watch?v=syjTFmLY2T4)  
- [Volatility 3: The volatile memory extraction framework](https://github.com/volatilityfoundation/volatility3)  
- [AVML утилита для снятия дампа оперативной памяти RAM](https://github.com/microsoft/avml)  
- [Примеры работы с Volatility](https://docs.google.com/document/d/1v7u6HVrae1R4fCCs1SNAGryjy5tmJCPDKq2Hyhqd9Fo/edit?usp=sharing)  

## 1) Основные методы HTTP    
_1_ GET - метод запрашивающий предоставление данных от сервера. Запросы при использовании этого метода могут только запрашивать данные, но не могут изменять состояние сервера.  

Метод используется для:  
- получения HTML страниц для отображения в браузере   
- запрос JSON данных для динамических приложений (прим: получение списка пользователей или товаров)  
- загрузка изображений и ведео, также других медиафайлов  
- поиск по ключевым словам  

Пример GET-запроса  
>GET /index.html HTTP/1.1  
Host: www.example.com  
User-Agent: Mozilla/5.0  
Accept: text/html  

_2_ HEAD - метод запрашивающий заголовки ресурса, также как метод GET, но без тела ресурсов. Метод полезен для извлечения метаданных сервера.  
_3_ POST - используется для отправки данных на сервер, что может вызывать измнение сосстояния сервера. Используется для отправки форм на веб-сайте.  

Пример POST-метода  
>POST /submit HTTP/1.1  
Host: www.example.com  
Content-Type: application/x-www-form-urlencoded  
Content-Length: 27  
username=user&password=pass123  


_4_ PUT - метод используется для создания нового ресурса или замены существующего по указанному URI. Метод может быть использован как для обновления, так и для создания ресурса.  
_5_ DELETE - удаляет указанный ресурс с сервера.  
_6_ CONNECT - метод устанавливает туннель между клиентом и сервером, используется для создания защищенного прокси соединения.  
_7_ OPTIONS - метод использующийся для описания параметров соединения (доступные методы, заголовки и т д). Позволяет клиенту узнать, какие методы поддерживает сервер.   
_8_ TRACE - выполняет вызов возвращаемого тестового сообщения с ресурса, позволяя клиенту видеть, как запрос проходит через промежуточные узлы.  
_9_ PATH - метод используется для частичного изменения ресурсов, позволяя обновлять только те части, которые требуют изменения.  



## 2) Установка Volatility  
- копируем репозиторий с гитхаба и переходим в папку    
```   
git clone https://github.com/volatilityfoundation/volatility3.git  
cd volatility3  
``` 

- устанавливаем и обновляем python3  
``` 
sudo apt update  
sudo apt install python3-full -y  
sudo apt install python3-pip  
``` 

- запускаем виртуальное окружение  
``` 
python3 -m venv venv  
source venv/bin/acivte  
pip3 install -r requirements.txt  
``` 

## 3) Установка AVML, снятие дампа и его просмор в Volatility  
### 3.1 Установка AVML  
- устанавливаем нужные утилиты и качаем файл с репозитория github  

```  
sudo apt install curl wget  
wget https://github.com/microsoft/avml/releases/download/v0.14.0/avml  
```   

- даем права на выполнение скрипта и перемещаем его в директорию вызова скриптов  

```  
chmod +x avml  
sudo mv avml /usr/local/bin  
```   
 
### 3.2 Снятие дампа оперативной памяти при помощи AVML  
- для снятия дампа используем команду:  
``` 
sudo avml kali_dump.dmp  
``` 

- результат в корневой директории сохраняется файл снятого дампа:  
![AVML_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_25/img/AVML_1.png)  

### 3.3 просмотр дампа памяти при помощи Volatility  
- проверяем какое в системе ядро следующей командой:  

```   
uname -a    
```   
![AVML_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_25/img/AVML_2.png)  

- используем volatility для оработки дампа kali_dump.dmp  
- выводим перечень доступных команд в volatility  

``` 
sudo python3 vol.py -f ~/kali_dump.dmp a  
``` 
![AVML_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_25/img/AVML_3.png)  

- применяем команду banners.Banners  
```   
sudo python3 vol.py -f ~/kali_dump.dmp banners.Banners  
``` 
![AVML_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_25/img/AVML_4.png)  





