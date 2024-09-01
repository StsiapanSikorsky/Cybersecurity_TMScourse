# Домашнее задание 7 - типы атак OWASP top 10  
**1) Изучение SQL запросов**  
- [Прохождение заданий в SQLBOLT](https://sqlbolt.com/)  

**2)  Лабораторные работы по OWASP top 10**
- Лабораторные работы из практики Broken Access Control   
[Lab Broken Access Control_1](https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter)  
- Лабораторные работы из практики SQL-Injections  
[Lab SQL-Injection_1](https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data)
- Лабораторная работа из практики Server-Side Request Forgery  
[Lab SSRF_1](https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost)

**3) Тренировка поиска уязвимостей на примере OWASP Juice Shop**
- [OWASP Juice Shop](https://spy-soft.net/owasp-juice-shop/)

 ## 1) Изучение SQL-запросов
 ### 1. Урок SQL 1 - запросы SELECT 101
 >[!NOTE]  
 SELECT - запрос языка SQL (извлечение записи из таблицы)  
 SELECT column1, column2 ... FROM tablename  
 SELECT * - извлечение всей таблицы

Отчет о выполнении задания 1
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgSQL/SQL_lesson1.png)

### 2. Урок SQL 2 - запросы с ограничениями Ч1
 
WHERE - оператор условия выполняющий фильтрацию запросов 

| Оператор | Состояние | Пример |
| :-------- | :--------------------------------------: | :------ |
|=, !=, <, <=, >, >= |операторы условий|column != 4|
|BETWEEN...AND...|нахождение в диапазоне значений включительно|column BETWEEN 1.5 AND 10.5|
|NOT BETWEEN...AND|нахождение за пределами диапазона значений включительно|-|
|IN (...)|номер находится в списке|column IN (2,4,5)|
|NOT IN(...)|номер не находится в списке|column NOT IN(1,3,4)|  

>[!IMPORTANT]  
Пример структуры запроса:
SELECT Id, Title FROM mytable WHERE ID = 6

Отчет о выполнении задания 2   
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgSQL/SQL_lesson2.png)  

### 3. Урок SQL 3 - запросы с ограничениями Ч2  

| Оператор | Состояние | Пример |
| :-------- | :--------------------------------------: | :------ |
|=         | точное сравнение строк с учетом регистра | column = "abc" | 
| != или <>| точное сравнение строковых неравенств  с учетом регистра | column != "abc" |
| LIKE | точное сравнение строк без учета регистра (до первого совпадения) | column LIKE "ABC" | 
| NOT LIKE | точное сравнение строковых неравенств без учета регистра | column NOT LIKE "ADCD" |
| % | используется в любом месте строки для сопоставления последовательности из нуля и более символов (только с LIKE или NOT LIKE) Тоесть если есть совпадение подстроки в строке, то выводим результат | column LIKE "%AT%" (matches "AT","ATTIC","CAT" or even "BATS") |
| _ | используется в любом месте строки для сопоставления одного символа (только с LIKE или NOT LIKE) | column LIKE "AN_" (matches "AND", but not "AN") |
| IN(...) | строка существует в списке | column IN ("A","B","C") |
| NOT IN(...) | строка не существует в списке | column NOT IN ("D","E","F") |

>[!IMPORTANT]  
Примеры вывода:  
SELECT Title FROM movies WHERE Title LIKE "%Toy Story%";  
SELECT Title, Director FROM movies WHERE Director = "John Lasseter";  
SELECT Title, Director FROM movies WHERE Director NOT LIKE "John Lasseter";  

Отчет о выполнении задания 3  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgSQL/SQL_lesson3.png)  

### 4. Урок SQL 4 - фильтрация и сортировка результатов запроса
>[!NOTE]  
DISTINCT -  ключевое слово, позволяющее отбрасывать строки, содержающие значения столбца  
Пример:  
SELECT DISTINCT column1, column2 FROM mytable WHERE ...  

>[!NOTE]  
ORDER BY - ключевое слово, позволяющее сортировать результаты по заданному столбцу. Когда JRDER BY указано, каждая строка сортируется в алфавитно цифровом порядке, на основе указанного значения столбца. (ORDER BY column ASC/DESC (DESC-в порядке убывания))  
LIMIT - ключевое слово позволяющее уменьшать число возвращаемых строк (LIMIT num_limit)
OFFSET - ключевое слово позволяющее вести счет числовых рядов начиная с (OFFSET num_offset)

>[!IMPORTANT]  
Примеры вывода:  
SELECT Title, Year FROM Movies ORDER BY Year DESC LIMIT 5;  
SELECT Title FROM Movies ORDER BY Title ASC LIMIT 5;  
SELECT Title FROM Movies ORDER BY Title ASC LIMIT 5 OFFSET 5;

Отчет о выполнении задания 4:  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgSQL/SQL_lesson4.png)  

### 5. Обзор SQL - простые запросы SELECT
Отчет о выполнении задания 5:  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgSQL/SQL_lesson5.png)  

### 6. Многотабличные запросы с соединениями JOIN  
Нормализация - разбиение таблиц на несколько ортогональных частей.

JOIN - ключевое слово необходимое для подключения сторонней таблицы (все сторонние условия WHERE, ORDER BY ставятся после).  
ON - ключевое слово предназначенное для совмещения колонок таблиц (обычно их ID)

>[!IMPORTANT]  
SELECT title, domestic_sales, international_sales FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id;
SELECT title, domestic_sales, international_sales FROM movies JOIN boxoffice ON movies.id = boxoffice,movie_id WHERE international_sales > domestic_sales;  
SELECT title, rating FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id ORDER BY Rating DESC;   

![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgSQL/SQL_lesson7.png)  

### 7. Внешние соединения  
В случае, если данные в таблицах имеют не симметричный характер, то необходимо использовать модификаторы: **INNER/LEFT/RIGHT/FULL JOIN**  

>[!IMPORTANT]  
SELECT DISTINCT Building FROM Employees;  
SELECT DISTINCT Building_name, Role FROM Buildings LEFT JOIN Employees ON Buildings.Building_name = Employees.Building;  

![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgSQL/SQL_lesson7.png)  

### 8. Краткое замечание о значениях NULL  
>[!IMPORTANT]  
SELECT Name, Role FROM employees WHERE building IS NULL  
SELECT DISTINCT Building_name, Role FROM Buildings LEFT JOIN Empoyees ON Building_name = Building WHERE Role IS NULL    
![image]()  


### 9. Запросы с выражениями  







## 2) Лабораторные работы OWASP top 10  
### 2.1 Broken Access Control  
Цель: получение доступа с правами администратора на сервисе и удаление пользователя **carlos**

- При попытке получения доступа к /admin путем простого добавления пользователя в аддресную строку, был получен отказ в доступ  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab1_0.png)  

- Просмотр файлов Cookie на сайте показал заданное значение false для поля administrator, после чего значение было изменено  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab1_1.png)

- В результате был получен доступ к сайту от имени администратор и можно было приступать к удалению пользователя carlos  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab1_2.png)  

- После проделанных действий лабораторная работа была успешно выполнена  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab1_3.png)  

### 2.2 SQL-Injection
Цель: извлечение скрытых данных путем внедрения SQL инъекции в предложение WHERE

- Заходим в любой раздел на эмулированом сайте
- В строке ввода адреса сервера после **cathegory** прописываем следующий результат запроса: 
> '+OR+1=1 --

- В результате обновления страницы, получаем список скрытых товаров и отчет о выполнении лабораторной работы   
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/SQL_lab1_2.png)  

### 2.3 Service - Side Request Forgery  
Подделка запросов на стороне сервера (SSRF) - уязвимость веб-безопасности, позволяющая злоумышленнику заставить серверное приложение отправлять запросы в непредусмотренное место. 

Злоумышленник может заставить сервер подключиться к внутренним службам в инфроструктуре организации, либо произвольным внешним службам. (Происходит утечка учетных данных авторизации)  

####  Ход выполнения лабораторной работы  
Цель: путем подделки запросов удалить пользователя **carlos**     
- При попытке получения доступа к /admin путем простого добавления пользователя в аддресную строку, был получен отказ в доступе   
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab3_1.png)  

- Переходим на страницу товара и получаем данные о количестве товара
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab3_2.png)  

- При этом осуществляем перехвать запроса и ответа сервера  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab3_3.png)

- Заменяем stockAPI запрос на сервер http://localhost. В ответе находим дерикторию /admin и подключаемся к ней  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab3_4.png)  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab3_5.png)  

- Графически отображаем дерикторию админа  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab3_6.png)  

- Копируем путь удаления пользователя carlos и отправляем запрос  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab3_7.png)

- Отчет об успешно выполненной работе  
![image](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task7/imgLabsa/lab3_8.png)  




## 3) Тренировка поиска уязвимостей на примере OWASP Juice Shop
### 3.1 Установка docker на ВМ KaliLinux
>sudo apt update  
sudo apt install -y docker.io  
sudo systemctl enable docker --now  
sudo usermod -aG docker $USER  
sudo apt-get install ca-certificates curl  
sudo install -m 0755 -d /etc/apt/keyrings  
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc  
sudo chmod a+r /etc/apt/keyrings/docker.asc  
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin  

Результат установки и версия Docker:  
![image]()

### 3.2 Установка Juice Shop 
Установка описанна по следующей ссылке: [Установка JuiceShop](https://hub.docker.com/r/bkimminich/juice-shop)  

Для скачивания образа docker используем команду docker pull
>docker pull bkimminich/juice-shop  

После запускаем docker командой run на 80 локальном порту (3000 в docker) используя команду:  
>docker run -d -p 80:3000 bkimminich/juice-shop  
![image]()  

Как результат по адресу localhost:80 открывает JuiceShop в браузере  
![image]()  

Используя адрес ВМ KaliLinux (10.10.0.6) заходим на JuiceShop в ВМ Windows10  
![image]()  




















