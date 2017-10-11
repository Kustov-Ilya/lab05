[![Build Status](https://travis-ci.org/Kustov-Ilya/lab05.svg?branch=master)](https://travis-ci.org/Kustov-Ilya/lab05)
## Laboratory work V

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**

```ShellSession
$ open https://travis-ci.org
```

## Tasks

- [x] 1. Авторизоваться на сервисе **Travis CI** с использованием **GitHub** аккаунта
- [x] 2. Создать публичный репозиторий с названием **lab05** на сервисе **GitHub**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Включить интеграцию сервиса **Travis CI** с созданным репозиторием
- [x] 5. Получить токен для **Travis CLI** с правами **repo** и **user**
- [x] 6. Получить фрагмент вставки значка сервиса **Travis CI** в формате **Markdown**
- [x] 7. Установить [**Travis CLI**](https://github.com/travis-ci/travis.rb#installation)
- [x] 8. Выполнить инструкцию учебного материала
- [x] 9. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

Создание переменных окружения
```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_TOKEN=<полученный_токен>
```
Клонирование репозитория lab04 в новый lab05
```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab04 lab05
$ cd lab05
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab05
```
Редактирование travis.yml: язык
```ShellSession
$ cat > .travis.yml <<EOF
language: cpp
EOF
```
Редактирование travis.yml: скрипт
```ShellSession
$ cat >> .travis.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
```
Редактирование travis.yml: аддоны
```ShellSession
$ cat >> .travis.yml <<EOF

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```
Записываем токен
```ShellSession
$ travis login --github-token ${GITHUB_TOKEN}
```
Проверка .travis.yml
```ShellSession
$ travis lint
```
Вставка значка в README.md
```ShellSession
$ ex -sc '1i|<фрагмент_вставки_значка>' -cx README.md
```
Коммит
```ShellSession
$ git add .travis.yml
$ git add README.md
$ git commit -m"added CI"
$ git push origin master
```
Использование комманды тревиса 
```ShellSession
$ travis lint  #check for warnings in travis.yml
Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping

$ travis accounts  #показывает соединенные GitHub аккаунты
Kustov-Ilya (Kustov-Ilya): subscribed, 5 repositories

$ travis sync  #синхронизация
synchronizing: .. done

$ travis repos  #отображение репозиториев
Kustov-Ilya/2-Semester (active: no, admin: yes, push: yes, pull: yes)
Description: ???
Kustov-Ilya/3-Semester (active: no, admin: yes, push: yes, pull: yes)
Description: ???
Kustov-Ilya/lab03 (active: no, admin: yes, push: yes, pull: yes)
Description: ???
Kustov-Ilya/lab04 (active: no, admin: yes, push: yes, pull: yes)
Description: ???
Kustov-Ilya/lab05 (active: yes, admin: yes, push: yes, pull: yes)
Description: ???

$ travis enable  # добавить travis в текущей директории
Detected repository as Kustov-Ilya/lab05, is this correct? |yes| 
Kustov-Ilya/lab05: enabled :)

$ travis whatsup  #показывает пройденные шаги
Kustov-Ilya/lab05 started: #1

$ travis branches  #показывает  шаги в master 
master:  #1    passed     added CI

$ travis history  #показывает  историю изменений 
#1 passed:       master added CI

$ travis show #показывает  информацию
Job #1.1:  added CI
State:         passed
Type:          push
Branch:        master
Compare URL:   https://github.com/Kustov-Ilya/lab05/compare/89aa3e2d8fa0^...515a03d5f8dc
Duration:      1 min 10 sec
Started:       2017-10-11 18:12:58
Finished:      2017-10-11 18:14:08
Allow Failure: false
Config:        os: linux

```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=05
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [Travis Client](https://github.com/travis-ci/travis.rb)
- [AppVeyour](https://www.appveyor.com/)
- [GitLab CI](https://about.gitlab.com/gitlab-ci/)

```
Copyright (c) 2017 Братья Вершинины
```
