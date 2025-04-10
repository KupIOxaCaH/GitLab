# Домашнее задание к занятию "`GitLab`" - `Бойко Кирилл`

---

### Задание 1

**Что нужно сделать:**

1. Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в [этом репозитории](https://github.com/netology-code/sdvps-materials/tree/main/gitlab).   
2. Создайте новый проект и пустой репозиторий в нём.
3. Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.

В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.


 
---

#### Решение 1  
  
*Работающий runner*  
![Работающий runner](https://github.com/KupIOxaCaH/GitLab/blob/main/img/1.PNG)  
![Работающий runner](https://github.com/KupIOxaCaH/GitLab/blob/main/img/2.PNG)  
![Работающий runner](https://github.com/KupIOxaCaH/GitLab/blob/main/img/3.PNG)  
*Настройки runner*  
![Настройки runner](https://github.com/KupIOxaCaH/GitLab/blob/main/img/4.PNG)
  
---

### Задание 2

**Что нужно сделать:**

1. Запушьте [репозиторий](https://github.com/netology-code/sdvps-materials/tree/main/gitlab) на GitLab, изменив origin. Это изучалось на занятии по Git.
2. Создайте .gitlab-ci.yml, описав в нём все необходимые, на ваш взгляд, этапы.

В качестве ответа в шаблон с решением добавьте: 
   
 * файл gitlab-ci.yml для своего проекта или вставьте код в соответствующее поле в шаблоне; 
 * скриншоты с успешно собранными сборками.


---

#### Решение 2  

*Выполненый pipilene*  
![Выполненый pipilene](https://github.com/KupIOxaCaH/GitLab/blob/main/img/5.PNG)

*Код pipilene:*  
  
stages:
  - test
  - analyze

test_job:
  stage: test
  script:
    - echo "Запуск тестов Go..."
    - go test .
    - echo "Тесты выполнены успешно!"
  only:
    - main

analyze_job:
  stage: analyze
  script:
    - echo "Лёгкий анализ без зависимостей:"
    - echo "1. Проверка синтаксиса:"
    - find . -name '*.go' -exec gofmt -l {} \; | grep -v vendor/ || true
    - echo "2. Подсчёт строк кода:"
    - find . -name '*.go' | xargs wc -l
    - echo "3. Проверка на наличие TODO:"
    - grep -rn "TODO" . || true
    - echo "Анализ завершён!"

  
---

### Задание 3*

**Что нужно сделать:**

Измените CI так, чтобы:

 - этап сборки запускался сразу, не дожидаясь результатов тестов;
 - тесты запускались только при изменении файлов с расширением *.go.

В качестве ответа добавьте в шаблон с решением файл gitlab-ci.yml своего проекта или вставьте код в соответсвующее поле в шаблоне.

---

#### Решение 3  
  
  
