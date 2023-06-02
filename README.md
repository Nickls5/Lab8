## Laboratory work VI


## Homework

Клонировал репозиторий от лабораторной работы №4 и переключился лабораторной работы №6
```console
nikls@nikls-VirtualBox:~$ mkdir Lab6
nikls@nikls-VirtualBox:~$ cd Lab6
nikls@nikls-VirtualBox:~/Lab6$ cd
nikls@nikls-VirtualBox:~$ git clone https://github.com/Nickls5/lab4 Lab6
Клонирование в «Lab6»...
remote: Enumerating objects: 78, done.
remote: Counting objects: 100% (78/78), done.
remote: Compressing objects: 100% (59/59), done.
remote: Total 78 (delta 14), reused 65 (delta 10), pack-reused 0
Получение объектов: 100% (78/78), 39.06 КиБ | 850.00 КиБ/с, готово.
Определение изменений: 100% (14/14), готово.
nikls@nikls-VirtualBox:~/Lab6$ git remote remove origin
nikls@nikls-VirtualBox:~/Lab6$ git remote add origin https://github.com/Nickls5/Lab06
```

- Добавил *CMakeLists.txt*
```console
nikls@nikls-VirtualBox:~/Lab6$ cat > CMakeLists.txt
cmake_minimum_required(VERSION 3.4)
project(Lab6)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include_directories("formatter_lib")
include_directories("formatter_ex_lib")
include_directories("solver_lib")

add_library(formatter_lib STATIC "formatter_lib/formatter.cpp")
add_library(formatter_ex_lib STATIC "formatter_ex_lib/formatter_ex.cpp")
add_library(solver_lib STATIC "solver_lib/solver.cpp")

add_executable(solver "solver_application/equation.cpp")

target_link_libraries(solver solver_lib formatter_ex_lib formatter_lib)

include(CPackConfig.cmake)
^Z
[1]+  Остановлен    cat > CMakeLists.txt
```
- Добавил *CPackConfig.cmake*
```console
nikls@nikls-VirtualBox:~/Lab6$ cat > CPackConfig.cmake
include(InstallRequiredSystemLibraries)
set(CPACK_PACKAGE_CONTACT donotwriteme@bmstuisbetterthanhse.com)
set(CPACK_PACKAGE_VERSION_MAJOR \${PRINT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR \${PRINT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH \${PRINT_VERSION_PATCH})
set(CPACK_PACKAGE_VERSION_TWEAK \${PRINT_VERSION_TWEAK})
set(CPACK_PACKAGE_VERSION \${PRINT_VERSION})

set(CPACK_RESOURCE_FILE_LICENSE \${CMAKE_CURRENT_SOURCE_DIR}/LICENSE)
set(CPACK_RESOURCE_FILE_README \${CMAKE_CURRENT_SOURCE_DIR}/README.md)
set(CPACK_RPM_PACKAGE_NAME "solver_lab")
set(CPACK_RPM_PACKAGE_LICENSE "MIT")
set(CPACK_RPM_PACKAGE_GROUP "solver")
set(CPACK_RPM_PACKAGE_VERSION CPACK_PACKAGE_VERSION)
set(CPACK_DEBIAN_PACKAGE_NAME "libsolvert-lab")
set(CPACK_DEBIAN_PACKAGE_PREDEPENDS "cmake >= 3.0")
set(CPACK_DEBIAN_PACKAGE_VERSION CPACK_PACKAGE_VERSION)
include(CPack)
^Z
[2]+  Остановлен    cat > CPackConfig.cmake
```

- Перестроил файл *CI.yml*
```console
nikls@nikls-VirtualBox:~/Lab6/.github/workflows$ rm CI.yml
nikls@nikls-VirtualBox:~/Lab6/.github/workflows$ cat > CI.yml
name: CMake

on:
 push:
  branches: [master]
  tags: -"v*1.*"
 pull_request:
  branches: [master]

env:

  BUILD_TYPE: Release
jobs: 
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    
    - name: Build
      run: cmake -H. -B_build -DCPACK_GENERATOR="TGZ" && cmake --build _build --target package &&
             cd _build && cpack -G "DEB" &&
             cpack -G "RPM" &&
             mkdir ../artifacts &&
             mv *.tar.gz ../artifacts/ &&
             mv *.deb ../artifacts/ &&
             mv *.rpm ../artifacts/
    - name: Publish
      uses: actions/upload-artifact@v2
      with:
        name: debrpm
        path: artifacts/

^Z
[3]+  Остановлен    cat > CI.yml
```

Запушил проект на сервер
```console
nikls@nikls-VirtualBox:~/Lab6/.github/workflows$ cd ..
nikls@nikls-VirtualBox:~/Lab6/.github$ cd ..
nikls@nikls-VirtualBox:~/Lab6$ git add .
nikls@nikls-VirtualBox:~/Lab6$ git commit -m "First commit"
[master bbd7b89] First commit
 48 files changed, 193 insertions(+), 3454 deletions(-)
 rewrite .github/workflows/CI.yml (92%)
 create mode 100644 CMakeLists.txt
 create mode 100644 CPackConfig.cmake
 rename formatter_ex_lib/{src => }/formatter_ex.cpp (95%)
 rename formatter_ex_lib/{src => }/formatter_ex.h (95%)
 rename formatter_lib/{build/CMakeFiles/3.22.1/CMakeDetermineCompilerABI_C.bin => .CMakeLists.txt.swp} (56%)
 mode change 100755 => 100644
 delete mode 100644 formatter_lib/build/CMakeCache.txt
 delete mode 100644 formatter_lib/build/CMakeFiles/3.22.1/CMakeCCompiler.cmake
 delete mode 100644 formatter_lib/build/CMakeFiles/3.22.1/CMakeCXXCompiler.cmake
 delete mode 100755 formatter_lib/build/CMakeFiles/3.22.1/CMakeDetermineCompilerABI_CXX.bin
 delete mode 100644 formatter_lib/build/CMakeFiles/3.22.1/CMakeSystem.cmake
 delete mode 100644 formatter_lib/build/CMakeFiles/3.22.1/CompilerIdC/CMakeCCompilerId.c
 delete mode 100755 formatter_lib/build/CMakeFiles/3.22.1/CompilerIdC/a.out
 delete mode 100644 formatter_lib/build/CMakeFiles/3.22.1/CompilerIdCXX/CMakeCXXCompilerId.cpp
 delete mode 100755 formatter_lib/build/CMakeFiles/3.22.1/CompilerIdCXX/a.out
 delete mode 100644 formatter_lib/build/CMakeFiles/CMakeDirectoryInformation.cmake
 delete mode 100644 formatter_lib/build/CMakeFiles/CMakeOutput.log
 delete mode 100644 formatter_lib/build/CMakeFiles/Makefile.cmake
 delete mode 100644 formatter_lib/build/CMakeFiles/Makefile2
 delete mode 100644 formatter_lib/build/CMakeFiles/TargetDirectories.txt
 delete mode 100644 formatter_lib/build/CMakeFiles/cmake.check_cache
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/DependInfo.cmake
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/build.make
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/cmake_clean.cmake
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/cmake_clean_target.cmake
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/compiler_depend.make
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/compiler_depend.ts
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/depend.make
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/flags.make
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/link.txt
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/progress.make
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/src/formatter.cpp.o
 delete mode 100644 formatter_lib/build/CMakeFiles/formatter_lib.dir/src/formatter.cpp.o.d
 delete mode 100644 formatter_lib/build/CMakeFiles/progress.marks
 delete mode 100644 formatter_lib/build/Makefile
 delete mode 100644 formatter_lib/build/cmake_install.cmake
 delete mode 100644 formatter_lib/build/libformatter_lib.a
 rename formatter_lib/{src => }/formatter.cpp (95%)
 rename formatter_lib/{src => }/formatter.h (94%)
 rename hello_world_application/{src => }/hello_world.cpp (92%)
 rewrite solver_application/CMakeLists.txt (63%)
 rename solver_application/{src => }/equation.cpp (94%)
 rename solver_lib/{src => }/solver.cpp (94%)
 rename solver_lib/{src => }/solver.h (96%)
nikls@nikls-VirtualBox:~/Lab6$ git push origin master
Username for 'https://github.com': Nickls5
Password for 'https://Nickls5@github.com': 
Перечисление объектов: 104, готово.
Подсчет объектов: 100% (104/104), готово.
При сжатии изменений используется до 2 потоков
Сжатие объектов: 100% (79/79), готово.
Запись объектов: 100% (104/104), 42.54 КиБ | 21.27 МиБ/с, готово.
Всего 104 (изменений 24), повторно использовано 77 (изменений 14), повторно использовано пакетов 0
remote: Resolving deltas: 100% (24/24), done.
To https://github.com/Nickls5/Lab06
 * [new branch]      master -> master
```

Создал tag
```console
nikls@nikls-VirtualBox:~/Lab6$ git tag v0.1.0.0
nikls@nikls-VirtualBox:~/Lab6$ git push origin master --tags
Username for 'https://github.com': Nickls5
Password for 'https://Nickls5@github.com': 
Перечисление объектов: 104, готово.
Подсчет объектов: 100% (104/104), готово.
При сжатии изменений используется до 2 потоков
Сжатие объектов: 100% (79/79), готово.
Запись объектов: 100% (104/104), 42.53 КиБ | 14.18 МиБ/с, готово.
Всего 104 (изменений 24), повторно использовано 77 (изменений 14), повторно использовано пакетов 0
remote: Resolving deltas: 100% (24/24), done.
To https://github.com/Nickls5/Lab06
 * [new tag]         v0.1.0.0 -> v0.1.0.0


```
Copyright (c) 2015-2021 The ISC Authors
```
