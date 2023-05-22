## Laboratory work IV

Для создания и запуска рабочего процесса GitHub Actions требуется только репозиторий GitHub. 

## Homework

Вы продолжаете проходить стажировку в "Formatter Inc." (см [подробности](https://github.com/tp-labs/lab03#Homework)).

В прошлый раз ваше задание заключалось в настройке автоматизированной системы **CMake**.

Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в [прошлый раз](https://github.com/tp-labs/lab03#Homework). Настройте сборочные процедуры на различных платформах:


- Создаю копию лабораторной работы №3.
- Привязываю копию к заранее созданному репозиторию "Lab04".
- Создаю каталог .github/workflows
- В этом каталоге создаю файл CI.yml
- Затем отправляю изменения на сервер.

```console
nikls@nikls-VirtualBox:~/Lab041$ mkdir .github
nikls@nikls-VirtualBox:~/Lab041$ cd .github
nikls@nikls-VirtualBox:~/Lab041/.github$ mkdir workflows
nikls@nikls-VirtualBox:~/Lab041/.github$ cd workflows
```
```console
nikls@nikls-VirtualBox:~/Lab041/.github/workflows$ cat > CI.yml
name: CMake

on:
 push:
  branches: [main]
 pull_request:
  branches: [main]

jobs: 
 build_Linux:

  runs-on: ubuntu-latest

  steps:
  - uses: actions/checkout@v3

  - name: Configure Solver
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

  - name: Build Solver
    run: cmake --build ${{github.workspace}}/solver_application/build

  - name: Configure HelloWorld
    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

  - name: Build HelloWorld
    run: cmake --build ${{github.workspace}}/hello_world_application/build

 build_Windows:

  runs-on: windows-latest

  steps:
  - uses: actions/checkout@v3

  - name: Configure Solver
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build

  - name: Build Solver
    run: cmake --build ${{github.workspace}}/solver_application/build

  - name: Configure HelloWorld
    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build

  - name: Build HelloWorld
    run: cmake --build ${{github.workspace}}/hello_world_application/build
^Z
[4]+  Остановлен    cat > CI.yml
```

```
Copyright (c) 2015-2021 The ISC Authors
```
