# Домашнее задание №29: Coding  
1) Ознакомиться с основными ресурсами по безопасной разработке  
2) Ознакомиться с информацией и написать скрипты на bash или python для проверки (password input validation) паролей и др  
- [Github проверки и валидации](https://github.com/sm1lexops/tms)  
3) Декодировать base64 файл в консоли Linux  
- JgBjAGgAYwBwAC4AYwBvAG0AIAA2ADUAMAAwADEAIAA+ACAAJABuAHUAbABsAAoAJABlAHgAZQBjAF8AdwByAGEAcABwAGUAcgBfAHMAdAByACAAPQAgACQAaQBuAHAAdQB0ACAAfAAgAE8AdQB0AC0AUwB0AHIAaQBuAGcACgAkAHMAcABsAGkAdABfAHAAYQByAHQAcwAgAD0AIAAkAGUAeABlAGMAXwB3AHIAYQBwAHAAZQByAF8AcwB0AHIALgBTAHAAbABpAHQAKABAACgAIgBgADAAYAAwAGAAMABgADAAIgApACwAIAAyACwAIABbAFMAdAByAGkAbgBnAFMAcABsAGkAdABPAHAAdABpAG8AbgBzAF0AOgA6AFIAZQBtAG8AdgBlAEUAbQBwAHQAeQBFAG4AdAByAGkAZQBzACkACgBJAGYAIAAoAC0AbgBvAHQAIAAkAHMAcABsAGkAdABfAHAAYQByAHQAcwAuAEwAZQBuAGcAdABoACAALQBlAHEAIAAyACkAIAB7ACAAdABoAHIAbwB3ACAAIgBpAG4AdgBhAGwAaQBkACAAcABhAHkAbABvAGEAZAAiACAAfQAKAFMAZQB0AC0AVgBhAHIAaQBhAGIAbABlACAALQBOAGEAbQBlACAAagBzAG8AbgBfAHIAYQB3ACAALQBWAGEAbAB1AGUAIAAkAHMAcABsAGkAdABfAHAAYQByAHQAcwBbADEAXQAKACQAZQB4AGUAYwBfAHcAcgBhAHAAcABlAHIAIAA9ACAAWwBTAGMAcgBpAHAAdABCAGwAbwBjAGsAXQA6ADoAQwByAGUAYQB0AGUAKAAkAHMAcABsAGkAdABfAHAAYQByAHQAcwBbADAAXQApAAoAJgAkAGUAeABlAGMAXwB3AHIAYQBwAHAAZQByAA=  

Ссылки на дополнительные ресурсы  
- [SSDEEP](https://ssdeep-project.github.io/ssdeep/usage.html)  
- [CEI "С" Coding Standard](https://wiki.sei.cmu.edu/confluence/display/c/SEI+CERT+C+Coding+Standard)  
- [NIST 800-218 Secure Software Development](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-218.pdf)  
- [OWASP Developer Guide](https://owasp.org/www-project-developer-guide/assets/exports/OWASP_Developer_Guide.pdf)  
- [SANS 25 Programming Errors](https://www.sans.org/top25-software-errors/)  

## 2) Скрипт на bash для password input validation

```bash
 #!/bin/bash
   
 read -p "Input password " password

 # Проверка длинны пароля
    if [ $password -lt 8 ]; then
        echo "password length is less than 8"
        exit
    fi

 # Проверка содержания строчных букв
    if ! [ $password =~ [a-z] ]; then
        echo "Password does not contain a letter"
        exit
    fi

 # Проверка содержания заглавных букв
    if ! [ $password =~ [A-Z] ]; then
        echo "Password does not contain a capital letter"
        exit
    fi

 # Проверка содержит ли пароль цифры
    if ! [ $password =~ [0-9] ]; then
        echo "The password does not contain numbers"
        exit
    fi

 # Проверка содержания спецсимвола
    if ! [ $password =~ [\!\@\#\$\%\^\&\*\(\)\_\+\-\=\[\]\{\}\;\:\,\.\/\<\>\?\|] ]; then
        echo "The password does not contain a special character"
        exit
    fi

    echo "Password is correct."
    exit
```   

## 3) Декодирование base64 в консоли  
- Для декодирования и вывода в консоль нужно написать следующую команду:  
```  
echo "запись в формате base64" | base64 --decode  
```

![base64_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_29/img/base64_1.png)   

