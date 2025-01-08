# Дипломный проект: автоматизировать процесс проверки url через virustotal  

Для автоматизации процесса проверки URL через virustotal необходимо пройти регистрацию на их сайте, а также воспользоваться встроенным API, который находится в нашем профиле (переменная в  коде: apikey).


## Код скрипта  

```python
#!/usr/bin/env python3
import requests
import json

input_url = str(input("Сканирование, введите URL который хотите просканировать \n"))

#Отправка HTTP POST запроса
api_url = "https://www.virustotal.com/vtapi/v2/url/scan"
params = dict (apikey = "6322a317fe297cf1b310189b2bf1261df2afd557181e8f6ffa66963f75b72bb2", url = input_url)
response = requests.post(api_url, data = params)

#Обработка ответа
if response.status_code == 200:
#преобразование объекта json в словарь python
    result = response.json()
    #print(json.dumps(result, sort_keys = False, indent = 4))
else:
    print("Ошибка", response.status_code)

#Получение id отчета из словаря python
report_id = result.get('scan_id')

#Получение отчета о сканировании по id
print("Отчет о сканированном URL:")
api_url = 'https://www.virustotal.com/vtapi/v2/url/report'
params = dict(apikey='6322a317fe297cf1b310189b2bf1261df2afd557181e8f6ffa66963f75b72bb2', resource = report_id)
response = requests.get(api_url, params = params)
if response.status_code == 200:
  result=response.json()
  #print(json.dumps(result, sort_keys = False, indent = 4))

#Обработка результата
false_count = 0
true_count = 0
for key in result['scans']:
    result_detection = str(result['scans'][key]['detected'])
    if result_detection == 'False':
        false_count += 1
    else:
        true_count += 1
        print('Обнаружено в антивирусе: ',key)


print('Опасность обнаружена в ', true_count,'антивирусах')
print(false_count,' антивирусов показали что URL безопасен')
```

## Результат работы скрипта  
![Virustotal_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/Virustotal_1.png)

Результат работы скрипта, полностью соответствует результатам на проверки URL на сайте  
![Virustotal_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Diplom_project/img/Virustotal_2.png)  