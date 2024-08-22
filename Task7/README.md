# Домашнее задание 7 - типы атак OWASP top 10  
**1) Изучение SQL запросов**  
- [Прохождение заданий в SQLBOLT]()  

**2)  Лабораторные работы по OWASP top 10**
- Лабораторные работы из практики Broken Access Control   
_1_. [Lab Broken Access Control_1]()  
_2_. [Lab Broken Access Control_2]()
- Лабораторные работы из практики SQL-Injections  
_1_. [Lab SQL-Injection_1]()
- Лабораторная работа из практики Server-Side Request Forgery  
_1_. [Lab SSRF_1]()

**3) Тренировка поиска уязвимостей на примере OWASP Juice Shop**
- [OWASP Juice Shop]()

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









