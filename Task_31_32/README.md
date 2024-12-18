# Домашнее задание №31-32: DevSecOps  
1) Ознакомиться с основными ресурсами по DevSecOps  
2) Создать аккаунт на Gitlab  
- Пройти туториал по работе в GitLab  
- Создать тестовый pipeline со всеми этапами DevSecOps согластно [статьи на Хабр](https://habr.com/ru/companies/yandex_cloud_and_infra/articles/738192/)  
- Для тестирования pipeline собрать docker container, сохранить как артефакт, максимально [кастемизировать pipeline](https://github.com/sm1lexops/Profile_challenges?tab=readme-ov-file#3-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-security-as-code-%D0%BE%D0%BF%D0%B8%D1%88%D0%B8%D1%82%D0%B5-%D0%BF%D0%BE%D1%80%D1%8F%D0%B4%D0%BE%D0%BA-%D0%B4%D0%B5%D0%B9%D1%81%D1%82%D0%B2%D0%B8%D0%B9-%D0%BF%D0%BE-%D0%B8%D0%BD%D1%82%D0%B5%D0%B3%D1%80%D0%B0%D1%86%D0%B8%D0%B8-gitlab-sast-%D0%B2-gitlab-cicd-pipeline-%D0%BF%D1%80%D0%B8%D0%B2%D0%B5%D0%B4%D0%B8%D1%82%D0%B5-%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-%D0%BD%D0%B5%D0%BE%D0%B1%D1%85%D0%BE%D0%B4%D0%B8%D0%BC%D1%8B%D1%85-%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D0%B9-%D0%B4%D0%BB%D1%8F-%D0%BE%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F-%D1%86%D0%B5%D0%BB%D0%B5%D0%B2%D1%8B%D1%85-%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82%D0%BE%D0%B2-%D1%81%D0%BA%D0%B0%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-%D0%B2%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%B8-%D0%B2%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B8-%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D1%8F-%D1%83%D0%B2%D0%B5%D0%B4%D0%BE%D0%BC%D0%BB%D0%B5%D0%BD%D0%B8%D0%B9)  

Ссылки на дополнительные ресурсы:  
- [Уязвимости Pypi Library](https://www.opennet.ru/opennews/art.shtml?num=55565)  
- [Основные этапы DevSecOps](https://habr.com/ru/companies/yandex_cloud_and_infra/articles/738192/)  
- [Пример gitlab CI|CD pipeline](https://github.com/sm1lexops/Profile_challenges?tab=readme-ov-file#3-%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-security-as-code-%D0%BE%D0%BF%D0%B8%D1%88%D0%B8%D1%82%D0%B5-%D0%BF%D0%BE%D1%80%D1%8F%D0%B4%D0%BE%D0%BA-%D0%B4%D0%B5%D0%B9%D1%81%D1%82%D0%B2%D0%B8%D0%B9-%D0%BF%D0%BE-%D0%B8%D0%BD%D1%82%D0%B5%D0%B3%D1%80%D0%B0%D1%86%D0%B8%D0%B8-gitlab-sast-%D0%B2-gitlab-cicd-pipeline-%D0%BF%D1%80%D0%B8%D0%B2%D0%B5%D0%B4%D0%B8%D1%82%D0%B5-%D0%BF%D1%80%D0%B8%D0%BC%D0%B5%D1%80-%D0%BD%D0%B5%D0%BE%D0%B1%D1%85%D0%BE%D0%B4%D0%B8%D0%BC%D1%8B%D1%85-%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D0%B9-%D0%B4%D0%BB%D1%8F-%D0%BE%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F-%D1%86%D0%B5%D0%BB%D0%B5%D0%B2%D1%8B%D1%85-%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82%D0%BE%D0%B2-%D1%81%D0%BA%D0%B0%D0%BD%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F-%D0%B2%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%B8-%D0%B2%D1%8B%D0%BF%D0%BE%D0%BB%D0%BD%D0%B5%D0%BD%D0%B8%D1%8F-%D0%B8-%D0%BF%D0%BE%D0%BB%D1%83%D1%87%D0%B5%D0%BD%D0%B8%D1%8F-%D1%83%D0%B2%D0%B5%D0%B4%D0%BE%D0%BC%D0%BB%D0%B5%D0%BD%D0%B8%D0%B9)  

## 2) Работа с GitLab  
### 2.1) Создание аккаунта    

[GitLab_1](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_31_32/img/GitLab_1.png)  

### 2.2) Создание нового проекта  
Для создания нового проекта следует перейти на вкладку поиска и далее **Viev all my projects**  

[GitLab_2](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_31_32/img/GitLab_2.png)  

После чего в открывшимся окне станет доступна вкладка  **New Project**

[GitLab_3](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_31_32/img/GitLab_3.png)  

### 2.3) Добавление файлов к существующему проекту, новой ветки
Для добавления файла к существующему проекту необходимо нажать на знак **"+"** в папке с проектом  

[GitLab_4](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_31_32/img/GitLab_4.png)  

## 2.4) Создание тестового pipeline с этапами DevSecOps  
- Добавление файла **.gitlab-ci.yml, файл необходим для автоматизации CI\CD  

[GitLab_5](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_31_32/img/GitLab_5.png)  

```yml
#GitLab CI/CD pipeline DevSecOps

stages:
    - pre-build
    - build
    - post-build
    - test-time
    - deploy

#Переменные
variables:
    NAME            : Stsiapan
    CICD_Version    : v1.0
    LOG_FILE_NAME   : log.txt

    

#Выполнение по умолчанию в каждой джобе
default:    
    #Передача переменной в следующую джобу
    artifacts:
        paths:
            - $LOG_FILE_NAME

#Джобы
pre-build_job:
    stage: pre-build
    #Команды выполнения джобы
    script:
        - echo "__Pre-build started__"
        #Запись текста в log.txt
        - echo "1) Pre_Build" >> $LOG_FILE_NAME

build_job:
    stage: build
    script:
        - echo "__Build started__"
        - echo "2) Build" >> $LOG_FILE_NAME        

post-build_job:
    stage: post-build
    script:
        - echo "__Post-build started__"
        - echo "3) Build" >> $LOG_FILE_NAME           

test-time_job1:
    stage: build
    script:
        - echo "__Test-time started__"
        - echo "4.1) Test-time" >> $LOG_FILE_NAME       

test-time_job2:
    stage: build
    script:
        - echo "__Test-time started__"
        - echo "4.2) Test-time" >> $LOG_FILE_NAME    

test-time_job3:
    stage: build
    #Запуск 3 теста, после выполнения 2 предыдущих
    needs: [test-time_job1, test-time_job2]
    script:
        - echo "__Test-time started__"
        - echo "4.3) Test-time" >> $LOG_FILE_NAME   
            
deploy_job2:
    stage: build
    #Если Брэнч коммит сделался в ветке main, только тогда запускаем
    rules:
        - if: $CI_COMMIT_BRANCH == "main"
    script:
        - echo "__Deploy started__"
        - echo "5) Deploy" >> $LOG_FILE_NAME
        - cat $LOG_FILE_NAME
                      
```

- Послкольку для запуска pipeline в GitLab необходима верификация по номеру телефона, которая в данное время невозможна для пользователей РБ и РФ, смонтированный тестовый pipeline не выполняется.  

![GitLab_6](https://github.com/StsiapanSikorsky/Cybersecurity_TMScourse/blob/main/Task_31_32/img/GitLab_6.png)  