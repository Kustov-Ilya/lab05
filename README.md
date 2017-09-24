## Laboratory work III

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [X] 1. Создать публичный репозиторий с названием **lab03** и с лиценцией **MIT**
- [X] 2. Ознакомиться со ссылками учебного материала
- [X] 3. Выполнить инструкцию учебного материала
- [X] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

Установка значений переменных окружения GITHUB_USERNAME и GITHUB_EMAIL
```ShellSession
$ export GITHUB_USERNAME=Kustov-Ilya
$ export GITHUB_EMAIL=kustoff.il@yandex.ru
$ alias edit=vim
```

Создание рабочего пространства
```ShellSession
$ mkdir lab03 && cd lab03  #создание директории и переход в нее
$ git init  #создание локального репозитория
$ git config --global user.name ${GITHUB_USERNAME}  #настройка данных
$ git config --global user.email ${GITHUB_EMAIL}
$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab03  #добавление удаленного репозитория
$ git pull origin master  #слияние данных из удаленной ветки
$ touch README.md  #создание файла
$ git status  #определение состояния файлов
$ git add README.md  #переводит файл в готовое состояние для коммита
$ git commit -m"added README.md"  #коммит
$ git push origin master  #отправление файлов
```

Добавить на сервисе **GitHub** в репозитории **lab03** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
```

Получение изменений
```ShellSession
$ git pull origin master
$ git log  #история коммитов
```

Создание директории 
```ShellSession
$ mkdir sources  #создание директории для файлов исходного кода
$ mkdir include  #создание директории для заголовочных файлов
$ mkdir examples  #создание директории для примеров
$ cat > sources/print.cpp <<EOF  #создание и редактирование файлов
```

Заполненение файлов
```ShellSession
#include <print.hpp>

void print(const std::string& text, std::ostream& out) {
  out << text;
}

void print(const std::string& text, std::ofstream& out) {
  out << text;
}
EOF
```

Заполнение заголовочных файлов
```ShellSession
$ cat > include/print.hpp <<EOF
#include <string>
#include <fstream>
#include <iostream>

void print(const std::string& text, std::ostream& out = std::cout);
void print(const std::string& text, std::ofstream& out);
EOF
```

Первый пример
```ShellSession
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv) {
  print("hello");
}
EOF
```

Второй пример
```ShellSession
$ cat > examples/example2.cpp <<EOF
#include <fstream>
#include <print.hpp>

int main(int argc, char** argv) {
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

Редактирование README.md
```ShellSession
$ edit README.md
```
Добавление изменений
```ShellSession
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=03
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2017 Братья Вершинины
```
