# Домашнее задание №17: Защита инфраструктуры приложений  
1) Исследуем **Docker**  
- Скачать образ ubuntu:18.04 с hub.docker.io, проверить целостность и соответствие контрольной суммы SHA256  
- С помощью команды **docker image ls** отобразить все docker образы на системе, добавить в группу docker вашего пользователя для запуска команд docker без sudo  
- Запустить данный образ в интерактивном режиме в оболочке sh docker run -it < image name > sh  
- Внутри контейнера выполнить команду **whoami** для определения пользователя, под которым запусили контейнер  
- Запустить контейнер под пользователем tms  
- Прогнать образ через один из сканеров безопасности, проанализировать результаты:  
- [https://github.com/quay/clair](https://github.com/quay/clair)  
- [https://github.com/aquasecurity/trivy](https://github.com/aquasecurity/trivy)  

2) *Пишем Dockerfile  
- Скачать и видоизменить файл конфигурации nginx.conf, файл должен выводить **"Welcome to the TMS Cybersecurity Course"**   
- Создать Dockerfile с базовым образом **ubuntu:20.04**, в котором устанавливаем Nginx веб сервер, а затем копируем заранее скаченный файл конфигурации nginx.conf во внутрь директории nginx контейнера   
- Запускаем контейнер перебрасывая 8800 порт хоста на 80 порт контейнера   
- Вывод 127.0.0.1:8800 в браузере и скриним  

Ссылки на дополнительные ресурсы  
- [Docker run команды и флаги](https://docs.docker.com/engine/containers/run/)  


## 1) Исследуем Docker  
### 1.1 Скачивание образа ubuntu:20.04  
Заходим на **Docker hub** и во вкладке **Images** пишем ubuntu. Переходим по первой ссылке и для скачивания конкретной верссии по тэгу перехоим во вкладку **Tags**, находим нужный образ  
![docker_0](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/docker_0.png)  

Заходим скачиваем ubuntu:22.04  
>docker pull ubuntu:22.04  

![docker_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/docker_1.png)   

### 1.2 Просмотр результатов скачвания образа  
Просматриваем контрольную сумму скаченного образа командой
>docker inspect ubuntu:22.04  

![docker_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/docker_2.png)   

На докер хабе в тэге скаченного образа переходим на нужную архитектуру (linux/amd64)  
![docker_2.1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/docker_2.1.png)  

И сравниваем контрольную сумм с RepoDigests  
![docker_2.2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/docker_2.2.png)  

Также вытыщить RepoDigests из json файла можно следующей командой  
>docker inspect ubuntu:22.04 | jq '.[0].RepoDigests[0]'  

![docker_2.3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/docker_2.3.png)  

Отображаем все скаченные образы docker  
>docker image ls  

![docker_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/docker_3.png)  

Добавление пользователя в группу docker было осуществлено ранее (Task 7) командой  
>sudo usermod -aG docker $USER  

### 1.3 Запуск скаченного образа в интерактивном режиме в оболочке **sh**  
Для запуска образа в интерактивном режиме и оболочке sh используем следующую команду  
>docker run -it ubuntu sh  

![docker_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/docker_4.png)  

### 1.4 Определяем пользователя, под которым запустили контейнер  
Используем команду внутри оболочки контейнера **whoami** - пользователь root  

![docker_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/docker_5.png) 

### 1.5 Запуск контейнера под пользователем tms  
- Заходим в контейнер под оболочкой bash и добавляем пользователя **tms**  
>useradd tms  

![tms_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/tms_1.png)  

- Коммитим изменения создавая новый образ ubuntu-tms  
>docker commit cac610892a39 ubuntu-tms  

![tms_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/tms_2.png)  

- Запускаем новый образ под пользователем tms, проверяем командой whoami      
>docker run -it --name home2 --user tms ubuntu-tms  

![tms_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/tms_3.png)  

### 1.6 Сканирование образа с помощью инструмента **trivy**  
- Устанавливаем инструмент  
>sudo apt install trivy  

- Сканируем айди контейнера  
>sudo trivy image 97271d29cb79  

![docker_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/docker_6.png)  

Во второй колонке отображают CVE систему установленной в контейнер


## 2) *Пишем Dockerfile 
### 2.1 Написание Dockerfile  
- создаем папку в домашней дериктории **Docker**  
- создаем и заполняем **Dockerfile** (за основу берем Ubuntu:22.04, открываем 80 порт на докере, апгрэйдим систему и устанавливаем nginx)  

![ngnix_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/nginx_1.png)  

- Собираем образ командой  
>docker build -t ubng:test  

![ngnix_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/nginx_2.png)

- Проверяем образ в списке образов  

![ngnix_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/nginx_3.png)  

### 2.2 Редактирование ngnix  
- Запускаем контейнер под оболочкой bash и пробрасываем 8800 порт хоста на 80 порт контейнера   
>docker run -it -p 8800:80 --name name ubng:test bash  

![ngnix_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/nginx_4.png)  

- переходим в директорию **/var/www/html/** и редактируем html файл домашней nginx страницы  

![nginx_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/nginx_5.png)    

- выходим командой **exec**  

- командой сморим айди докер контейнера и коммитим изменения  
>docker ps -a
docker commit 31dfc5f4f83b ubng-new  

- Проверяем новый созданный образ  
>docker image -a  

![nginx_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task17/img/nginx_6.png)  

- Редактируем Dockerfile и собираем новый образ, на основе закомиченного  

![nginx_7](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/nginx_7.png)  

![nginx_8](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/nginx_8.png)  

- Запускаем новый контейнер и отображаем резуьтаты в браузере по запросу **localhost:8800**    

![nginx_9](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/nginx_9.png)  
![nginx_10](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_17/img/nginx_10.png)  
