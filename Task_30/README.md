# Домашнее задание №30: Web Application Security  

1) Ознакомиться с основными ресурсами по web application security  
2) Установить WAF (nginx + Modsecurity)  
- установить и протестировать запрет тестовых запросов curl  
- [Nginx + Modsecurity WAF](https://opsshield.com/help/cpguard/install-modsecurity-with-nginx-on-debian-ubuntu/)  
- [Smirnov nginx + modsecurity github](https://github.com/sm1lexops/Profile_challenges?tab=readme-ov-file#5-%D0%BF%D1%80%D0%B5%D0%B4%D0%BB%D0%BE%D0%B6%D0%B8%D1%82%D0%B5-%D1%81%D1%85%D0%B5%D0%BC%D1%83-%D0%B8%D0%BD%D1%82%D0%B5%D0%B3%D1%80%D0%B0%D1%86%D0%B8%D0%B8-web-application-firewall-waf-%D0%B2-%D0%B8%D0%BD%D1%84%D1%80%D0%B0%D1%81%D1%82%D1%80%D1%83%D0%BA%D1%82%D1%83%D1%80%D0%B5-%D0%BD%D0%B0%D0%BF%D0%B8%D1%88%D0%B8%D1%82%D0%B5-%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8E-%D0%B4%D0%BB%D1%8F-%D0%B2%D0%BD%D0%B5%D0%B4%D1%80%D0%B5%D0%BD%D0%B8%D1%8F-waf-%D0%BD%D0%B0%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-modsecurity-%D0%B2-nginx-%D0%BD%D0%B0%D0%BF%D0%B8%D1%88%D0%B8%D1%82%D0%B5-%D0%BA%D0%BE%D0%BD%D0%BA%D1%80%D0%B5%D1%82%D0%BD%D1%8B%D0%B5-%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80%D1%8B-%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB-%D0%B1%D0%B5%D0%B7%D0%BE%D0%BF%D0%B0%D1%81%D0%BD%D0%BE%D1%81%D1%82%D0%B8-%D0%BA%D0%BE%D1%82%D0%BE%D1%80%D1%8B%D0%B5-%D0%B2%D1%8B-%D0%B1%D1%8B-%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D0%BD%D0%B8%D0%BB%D0%B8-%D0%B2-waf-%D0%BD%D0%B0%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-%D1%84%D0%B8%D0%BB%D1%8C%D1%82%D1%80%D0%B0%D1%86%D0%B8%D1%8F-sql-%D0%B8%D0%BD%D1%8A%D0%B5%D0%BA%D1%86%D0%B8%D0%B9-xss-%D0%B0%D1%82%D0%B0%D0%BA-%D0%B1%D0%BB%D0%BE%D0%BA%D0%B8%D1%80%D0%BE%D0%B2%D0%BA%D0%B0-%D0%B7%D0%B0%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85-%D0%BF%D0%B0%D1%82%D1%82%D0%B5%D1%80%D0%BD%D0%BE%D0%B2)    
3) *Развертывание [Готовой виртуалки Ubuntu + modsecurity](https://drive.google.com/file/d/12tO5SwSu43IJprim8BafCmF-aQb9-EfM/view)  
- Настройка сетевого адаптера в режиме моста (сетевой мост/network bridge)  
- Проверка ip ВМ  
- Запуск контейнера с уязвимым приложением  
- sudo docker run -d -p 8080:80 saurav7055/xvwa    
- Теперь приложение доступно по вдресу {ip сервера}:80/xvwa по всей домашней сети (если нет ограничения фаервола)  
- Вызвать 5 разных сработок WAF правил, применяя уязвимости в приложении  
- Прислать результаты сработки правил WAF и его ID (var/log/nginx/error.log)  

Ссылки на дополнительные ресурсы:  
- [Отличия WAF от VPS](https://stormwall.pro/resources/terms/general/waf)  
- [12 лучших WAF решений](https://dzen.ru/a/ZCrzuo293D16oGyd)  
- [Как установить modsecurity с nginx](https://www.tecmint.com/install-modsecurity-nginx-debian-ubuntu/)  
- [CRS (Core Rule Set) набор правил для modsecurity](https://coreruleset.org/)  
- [Встраивание modsecurity crs - Modsecurity Wiki](https://www.netnea.com/cms/nginx-tutorial-6_embedding-modsecurity/)  
- [Готовая виртуалка Ubuntu + modsecurity](https://drive.google.com/file/d/12tO5SwSu43IJprim8BafCmF-aQb9-EfM/view)  
- [Примеры WAF ByPass](https://www.ptsecurity.com/upload/corporate/ru-ru/analytics/PT-devteev-CC-WAF.pdf)  
- [OWASP ASVS стандарт для безопасной разработки Web](https://habr.com/ru/companies/acribia/articles/519050/)    
- [Xtreme Vulnerable Web Application (XVWA)](https://github.com/s4n7h0/xvwa)  

## 2) Установка ModeSecurity и Nginx
- Установка nginx  

```
sudo apt install nginx  
```  

- Загружаем исходный пакет nginx  

```
sudo chown kali:kali /usr/local/src/ -R
mkdir -p /usr/local/src/nginx
```
- Переходим в исходный каталог nginx и загружаем исходный пакет  

```
cd /usr/local/src/nginx/
sudo apt install dpkg-dev
apt source nginx
```  

- Проверяем загруженные файли и смотрим чтобы установленная версия nginx была одинаковая со скаченными файлами   

```
ll
sudo nginx -v  
```  

![ModSecurity_1]()    

- Установка libmodsecurity3  

```  
sudo apt install git
git clone --depth 1 -b v3/master --single-branch https://github.com/SpiderLabs/ModSecurity /usr/local/src/ModSecurity/
cd /usr/local/src/ModSecurity/
```  

- Устанавливаем зависимости сборки  

``` 
sudo apt install gcc make build-essential autoconf automake libtool libcurl4-openssl-dev liblua5.3-dev libpcre2-dev libfuzzy-dev ssdeep gettext pkg-config libpcre3 libpcre3-dev libxml2 libxml2-dev libcurl4 libgeoip-dev libyajl-dev doxygen
``` 

- Установка необходимых подмодулей  

``` 
git submodule init
git submodule update
```  

- Настройка среды сборки  

```
./build.sh
./configure
```  

- Компилируем исходный код (для 2 ядер)  

```
make -j2
sudo make install
```  

- Переходим в исходный каталог nginx  

```
cd /usr/local/src/nginx/nginx-1.26.0
```  

- Устанавливаем зависимости сборки nginx  

```
sudo apt build-dep nginx
sudo apt install uuid-dev
```  

- Настраиваем среду  

```
sudo ./configure --with-compat --with-openssl=/usr/include/openssl/ --add-dynamic-module=/usr/local/src/ModSecurity-nginx
```  
В ходе выполнения команды, должен создаться **Makefile**, содержащий в себе информацию, представленную на скриншоте

![ModSecurity_2]()  

- Создаем модуль ModSecuriy Nginx Connector и копируем его

```
sudo make modules
sudo cp objs/ngx_http_modsecurity_module.so /usr/share/nginx/modules/  
```  

- Редактируем файл nginx находящегося по пути  

```
sudo vim /etc/nginx/nginx.conf
```

- В открытый файл добавляем следующие строки (в места как на скриншоте)  

![ModSecurity_3]()  

```
load_module modules/ngx_http_modsecurity_module.so;

modsecurity on;
modsecurity_rules_file /etc/nginx/modsec/main.conf;
```  

- Создаем каталог для хранения файлов ModSecurity, копируем файл конфигурации и открываем его для редактирования  

```
sudo mkdir /etc/nginx/modsec/ 
sudo cp /usr/local/src/ModSecurity/modsecurity.conf-recommended /etc/nginx/modsec/modsecurity.conf
sudo vim /etc/nginx/modsec/modsecurity.conf
```   

Редактируем файл как указано на скриншотах  
![ModSecurity_4]()  
![ModSecurity_5]()  
![ModSecurity_6]()  

- Создаем файл main.conf  

```
sudo vim /etc/nginx/modsec/main.conf 
```  

Записываем в данный файл следующую строку  
```
Include /etc/nginx/modsec/modsecurity.conf
```  

- Копируем файл сопоставления Unicode  

``` 
sudo cp /usr/local/src/ModSecurity/unicode.mapping /etc/nginx/modsec/
``` 

- Проверяем конфигурацию nginx  

``` 
sudo nginx -t
``` 

Результат должен содержать сообщение об успешном прохождении теста  
![ModSecurity_7]()  

## 2.2) Включение правил OWASP  

- Загружаем последнюю версию OWASP CRS, извлекаем файл, перемещаем и переименовываем его  

``` 
wget https://github.com/coreruleset/coreruleset/archive/v3.3.4.tar.gz 
tar xvf v3.3.4.tar.gz 
sudo mv coreruleset-3.3.4/ /etc/nginx/modsec/ 
sudo mv /etc/nginx/modsec/coreruleset-3.3.4/crs-setup.conf.example /etc/nginx/modsec/coreruleset-3.3.4/crs-setup.conf 
``` 

- Открываем основной файл конфигураций и редактируем его  

```
sudo vim /etc/nginx/modsec/main.conf 
```

Добавляем следующие строки  
```
Include /etc/nginx/modsec/coreruleset-3.3.4/crs-setup.conf
Include /etc/nginx/modsec/coreruleset-3.3.4/rules/*.conf
```


