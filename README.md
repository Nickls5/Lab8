# lab04
Лабораторная работа №4

Буду использовать github actions

1) Копирую третью лабораторную работу git clone 

2) Перехожу в папку cd lab03

3) Разрушаю связь git remote remove origin

4) Привязываю к новому, заранее созданному репозиторию lab04 git remote add origin

5) Создаю директорию .github/workflows mkdir .github cd .github mkfir workflows cd workflows

6) Создаю nano CI.yml 

В редакторе 

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

    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/
    
    solver_application/build



  - name: Build Solver

    run: cmake --build ${{github.workspace}}/solver_application/build



  - name: Configure HelloWorld

    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/

    hello_world_application/build

  - name: Build HelloWorld
  
    run: cmake --build ${{github.

    workspace}}/hello_world_application/build

 build_Windows:

  runs-on: windows-latest

  steps:
  
  - uses: actions/checkout@v3
 
  - name: Configure Solver
 
    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}
    \solver_application/build

 
  - name: Build Solver

    run: cmake --build ${{github.workspace}}/solver_application/build


  - name: Configure HelloWorld

    run: cmake ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/
    
    hello_world_application/build

  - name: Build HelloWorld

    run: cmake --build ${{github.workspace}}/hello_world_application/build
    
    
   7)Заливаю на гит 
   
   $ git add .github

$ git commit -m "path"

$ git push origin main
