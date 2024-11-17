# Домашнее задание №23: Event Management  

1) Изучение лабораторных стенодов Splunk SIEM   
- [Лабораторная практика c SIEM систаемами](https://cyberdefenders.org/)  
2) Установка EFK стэка с помощью docker-compose  
- [Установка EFK](https://docs.fluentd.org/container-deployment/docker-compose)  
3) *Установка SIEM Wazuch с помощью docker-compose  
- [Установить Wazuch docker-compose](https://documentation.wazuh.com/current/deployment-options/docker/docker-installation.html)  

Ссылки на дополнительные ресурсы  
- [Сравнение SIEM систем](https://www.anti-malware.ru/compare/SIEM-systems)  
- [Работа auditd linux](https://www.redhat.com/sysadmin/configure-linux-auditing-auditd)  
- [Лабораторная практика с SIEM системами](https://cyberdefenders.org/)  
- [Pozitive портал обучения](https://lms.edu.ptsecurity.com/)  

## 1) Лабораторные стены Splunk SIEM
### 1.1 ЛР1 - Packet detective lab  
Описание: анализ файлов перехвата сетевого трафика при помощи программы WireShark
- анализ превышеющей сессии обмена пакетами SMB  
- аутентификация пользователя через кого получен доступ  
- поиск службы через которую происходил обмен файлов  
- измерение продолжительности связи между двумя хостами  
- поиск имени злоумышленника  
- поиск названия исполняемого файла  

Полезные команды в WireShark  
>smb2.filename contains ".exe" - поиск файла по протоколу SMB2, c расширением .exe  
ip.addr == 10.1.30.46 - поиск по IP адресу  
tcp.port == 80 - поиск по порту  

Отчет о выполненой работе  
![Lab_1]()  


### 1.2 ЛР2 - Yellow RAT lab  
Описание: анализ в **Virus Total** вредоносного файла, по хэшу  
- поиск названия вредоносного ПО  
- поиск общего имени файла  
- определение времени компиляции вредоноса  
- поиск встраиваемых вредоносных файлов  
- поиск С2 сервера, на каторый вредонос отправляет данные  

Отчет о выполненной работе  
![Lab_2]()  

## 2) Установка EFK в через docker-compose  
- Создаем директорию efk в к котором будут распологаться файлы  

>mkdir efk  

- В директории создаем файл docker-compose.yml и заполняем его как указано на скриншоте  

```
    services:
  web:
    image: httpd
    ports:
      - "80:80"
    links:
      - fluentd
    logging:
      driver: "fluentd"
      options:
        fluentd-address: localhost:24224
        tag: httpd.access

  fluentd:
    build: ./fluentd
    volumes:
      - ./fluentd/conf:/fluentd/etc
    links:
      - "elasticsearch"
    ports:
      - "24224:24224"
      - "24224:24224/udp"

  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.13.1
    container_name: elasticsearch
    environment:
      - "discovery.type=single-node"
    expose:
      - "9200"
    ports:
      - "9200:9200"

  kibana:
    image: docker.elastic.co/kibana/kibana:7.13.1
    links:
      - "elasticsearch"
    ports:
      - "5601:5601"
```

![EFK_1]()  

- Создаем директорию fluentd и вней Dockerfile, заполняем его как на скриншоте  

>mkdir fluentd  
cd fluentd  
vim Dockerfile  

![EFK_2]()  

- В директории fluentd создаем директорию conf в которо создаем и заполняем файл конфигурации fluentd.conf  

![EFK_3]()  


- Возвращаемся в директорию etc и поднимам контейнер в режиме демона командой  

>docker-compose up -d  

![EFK_4]()  

- Переходим по адресу **http://localhost:5601**  

![EFK_5]()  

![EFK_6]()  






