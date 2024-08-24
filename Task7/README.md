# Домашнее задание 7 - типы атак OWASP top 10  
**1) Изучение SQL запросов**  
- [Прохождение заданий в SQLBOLT](https://sqlbolt.com/)  

**2)  Лабораторные работы по OWASP top 10**
- Лабораторные работы из практики Broken Access Control   
_1_. [Lab Broken Access Control_1](https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter)  
_2_. [Lab Broken Access Control_2](https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter)
- Лабораторные работы из практики SQL-Injections  
_1_. [Lab SQL-Injection_1](https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data)
- Лабораторная работа из практики Server-Side Request Forgery  
_1_. [Lab SSRF_1](https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost)

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















