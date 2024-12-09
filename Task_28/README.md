# Домашнее задание №28: Coding  
1) Ознакомиться с основными ресурсами по безопасной разработке  
2) Установить SSDEEP на Linux  
- создать файл text.txt, добавить в него произвольный код  
- скопировать text.txt в файл bamboo.exe, добавить 1 символ в конец файла bamboo.exe: echo "1" >> bamboo.exe  
- вычислить hash test.txt, hash до и после изменения bamboo.exe  
- с помощью SSDEEP сравнить два файла  

Ссылки на дополнительные ресуры:  
- [SSDEEP](https://ssdeep-project.github.io/ssdeep/usage.html)  
- [SEI CERT Coding Standart](https://ssdeep-project.github.io/ssdeep/usage.html)  
- [NIST 800-218 Secure Software Development](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-218.pdf)  
- [OWASP Developer Guide](https://owasp.org/www-project-developer-guide/assets/exports/OWASP_Developer_Guide.pdf)  
- [SANS 25 Programming Errors](https://www.sans.org/top25-software-errors/)   

## 2) Установка SSDEEP на KaliLinux  
- Для установки необходимо выполнить команду:  
``` 
sudo apt install ssdeep
```  
![SSDEEP_1]()  

- Создаем файл text.txt и записываем в него произвольный код:  
```   
touch text.txt  
vim text.txt  
``` 
![SSDEEP_2]()  

- Создаем файл bamboo.exe, копируем в него содержимое предыдущего файла и добовляем в конец "1"  
``` 
cp text.txt bamboo.exe  
echo "1" >> bamboo.exe  
``` 

- Вычисляем хэш файлов (зеленым обведены отличия)  
``` 
ssdeep text.txt  
ssdeep bamboo.exe  
``` 
![SSDEEP_3]()  

- При удалении символа "1" из файла bamboo.exe и сравнении их хэшей, они являются идентичными  
![SSDEEP_4]()  