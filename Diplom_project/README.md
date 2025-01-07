# Дипломный проект: автоматизировать процесс проверки url через virustotal  

## Код скрипта (рабочий, но не допилен)  

```python

#!/usr/bin/env python3

import requests
import json

api_url = "https://www.virustotal.com/vtapi/v2/url/scan"  
params = dict (apikey = "6322a317fe297cf1b310189b2bf1261df2afd557181e8f6ffa66963f75b72bb2", url = "https://github.com/StsiapanSikorsky")

response = requests.post(api_url, data = params)  

if response.status_code == 200:
    result = response.json()
    print(json.dumps(result, sort_keys = False, indent = 4))
else:
    print("Ошибка", response.status_code)

```