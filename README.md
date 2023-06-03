## Laboratory work VIII


## Homework

Клонировал репозиторий от лабораторной работы №6 в папку от №8
```console
nikls@nikls-VirtualBox:~$ git clone https://github.com/tp-labs/lab08
Клонирование в «lab08»...
remote: Enumerating objects: 76, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 76 (delta 0), reused 0 (delta 0), pack-reused 73
Получение объектов: 100% (76/76), 951.66 КиБ | 2.45 МиБ/с, готово.
Определение изменений: 100% (22/22), готово.
nikls@nikls-VirtualBox:~$ cd lab08
```
```console
nikls@nikls-VirtualBox:~/lab08$ git remote remove origin
nikls@nikls-VirtualBox:~/lab08$ git remote add origin https://github.com/Nickls5/Lab8
nikls@nikls-VirtualBox:~/lab08$ git remote -v
origin	https://github.com/Nickls5/Lab8 (fetch)
origin	https://github.com/Nickls5/Lab8 (push)
```

Выполнил туториал:

```sh
$ cat > Dockerfile <<EOF
FROM ubuntu:18.04
EOF
```

```sh
$ cat >> Dockerfile <<EOF

RUN apt update
RUN apt install -yy gcc g++ cmake
EOF
```

```sh
$ cat >> Dockerfile <<EOF

COPY . print/
WORKDIR print
EOF
```

```sh
$ cat >> Dockerfile <<EOF

RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
RUN cmake --build _build
RUN cmake --build _build && cmake --install _build
EOF
```

```sh
$ cat >> Dockerfile <<EOF

ENV LOG_PATH /home/logs/log.txt
EOF
```

```sh
$ cat >> Dockerfile <<EOF

VOLUME /home/logs
EOF
```

```sh
$ cat >> Dockerfile <<EOF

WORKDIR _install/bin
EOF
```

```sh
$ cat >> Dockerfile <<EOF

ENTRYPOINT ./demo
EOF
```

```sh
$ docker build -t logger .
```

<details><summary>Output</summary>
 
```console
nikls@nikls-VirtualBox:~/lab08$ sudo docker build -t logger .
Sending build context to Docker daemon  172.5kB
Step 1/12 : FROM ubuntu:18.04
 ---> f9a80a55f492
Step 2/12 : RUN apt update
 ---> Using cache
 ---> 7642e85d85b3
Step 3/12 : RUN apt install -yy gcc g++ cmake
 ---> Using cache
 ---> 2879719d4d88
Step 4/12 : COPY . print/
 ---> 4cf6990f4dcb
Step 5/12 : WORKDIR print
 ---> Running in caa6fbe6913b
Removing intermediate container caa6fbe6913b
 ---> c43d19c944e0
Step 6/12 : RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
 ---> Running in 2a79c8a33b2d
-- The C compiler identification is GNU 7.5.0
-- The CXX compiler identification is GNU 7.5.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /print/_build
Removing intermediate container 2a79c8a33b2d
 ---> d2e823848951
Step 7/12 : RUN cmake --build _build
 ---> Running in 15ceb0fdfcc9
Scanning dependencies of target formatter_ex_lib
[ 12%] Building CXX object CMakeFiles/formatter_ex_lib.dir/formatter_ex_lib/formatter_ex.cpp.o
[ 25%] Linking CXX static library libformatter_ex_lib.a
[ 25%] Built target formatter_ex_lib
Scanning dependencies of target formatter_lib
[ 37%] Building CXX object CMakeFiles/formatter_lib.dir/formatter_lib/formatter.cpp.o
[ 50%] Linking CXX static library libformatter_lib.a
[ 50%] Built target formatter_lib
Scanning dependencies of target solver_lib
[ 62%] Building CXX object CMakeFiles/solver_lib.dir/solver_lib/solver.cpp.o
[ 75%] Linking CXX static library libsolver_lib.a
[ 75%] Built target solver_lib
Scanning dependencies of target solver
[ 87%] Building CXX object CMakeFiles/solver.dir/solver_application/equation.cpp.o
[100%] Linking CXX executable solver
[100%] Built target solver
Removing intermediate container 15ceb0fdfcc9
 ---> 621ad2382b26
Step 8/12 : RUN cmake --build _build && cmake --install _build
 ---> Running in 4ee05963970f
[ 25%] Built target formatter_ex_lib
[ 50%] Built target formatter_lib
[ 75%] Built target solver_lib
[100%] Built target solver
-- Configuring done
-- Generating done
-- Build files have been written to: /print/_build
Removing intermediate container 4ee05963970f
 ---> f68d7f932077
Step 9/12 : ENV LOG_PATH /home/logs/log.txt
 ---> Running in f0c2b82468bb
Removing intermediate container f0c2b82468bb
 ---> 8a7fd23412f9
Step 10/12 : VOLUME /home/logs
 ---> Running in 11e5f70299ca
Removing intermediate container 11e5f70299ca
 ---> e2d0169faa4d
Step 11/12 : WORKDIR _install/bin
 ---> Running in 550a54b191bb
Removing intermediate container 550a54b191bb
 ---> 641190387f7a
Step 12/12 : ENTRYPOINT ./demo
 ---> Running in d2d73ea634cf
Removing intermediate container d2d73ea634cf
 ---> 2328530460a4
Successfully built 2328530460a4
Successfully tagged logger:latest
```
 
</details>
  
```sh
$ docker images
```
```console
nikls@nikls-VirtualBox:~/lab08$ sudo docker images
REPOSITORY   TAG       IMAGE ID       CREATED              SIZE
logger       latest    2328530460a4   About a minute ago   334MB
<none>       <none>    0b9f45949692   5 minutes ago        334MB
<none>       <none>    0e90caafcde6   6 minutes ago        334MB
<none>       <none>    b444cd14583d   25 minutes ago       334MB
<none>       <none>    756bee322c7d   26 minutes ago       334MB
<none>       <none>    f797211c658e   32 minutes ago       334MB
<none>       <none>    48fd89700ae4   47 minutes ago       335MB
ubuntu       18.04     f9a80a55f492   4 days ago           63.2MB
```

```sh
$ mkdir logs
$ docker run -it -v "$(pwd)/logs/:/home/logs/" logger
text1
text2
text3
<C-D>
```

```sh
$ docker inspect logger
```

<details><summary>Output</summary>
 
```console
nikls@nikls-VirtualBox:~/lab08$ sudo  docker inspect logger
[sudo] пароль для nikls: 
[
    {
        "Id": "sha256:2328530460a48999b262100b911c5d0e28d5e89de1fdcb042d92daea5bc11279",
        "RepoTags": [
            "logger:latest"
        ],
        "RepoDigests": [],
        "Parent": "sha256:641190387f7a10a562e8c39b83764ecd7c42e5b530eb250769bb5a771bd01f6c",
        "Comment": "",
        "Created": "2023-06-03T10:07:07.861936733Z",
        "Container": "d2d73ea634cf0a7a76763d85ea4e423f0a85ca2c9a9a3fcf5dadc532f3e66ebb",
        "ContainerConfig": {
            "Hostname": "d2d73ea634cf",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LOG_PATH=/home/logs/log.txt"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "ENTRYPOINT [\"/bin/sh\" \"-c\" \"./demo\"]"
            ],
            "Image": "sha256:641190387f7a10a562e8c39b83764ecd7c42e5b530eb250769bb5a771bd01f6c",
            "Volumes": {
                "/home/logs": {}
            },
            "WorkingDir": "/print/_install/bin",
            "Entrypoint": [
                "/bin/sh",
                "-c",
                "./demo"
            ],
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "18.04"
            }
        },
        "DockerVersion": "20.10.24",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LOG_PATH=/home/logs/log.txt"
            ],
            "Cmd": null,
            "Image": "sha256:641190387f7a10a562e8c39b83764ecd7c42e5b530eb250769bb5a771bd01f6c",
            "Volumes": {
                "/home/logs": {}
            },
            "WorkingDir": "/print/_install/bin",
            "Entrypoint": [
                "/bin/sh",
                "-c",
                "./demo"
            ],
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "18.04"
            }
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 333847610,
        "VirtualSize": 333847610,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/snap/docker/common/var-lib-docker/overlay2/fd9105c97080bc8f1a80e0050415d4f6a2e2ffe208f2180c0f61b501f17e0dda/diff:/var/snap/docker/common/var-lib-docker/overlay2/52dc38d155e97fda851857207b8a699df96d56fe784d7ee4473a14a30783282f/diff:/var/snap/docker/common/var-lib-docker/overlay2/750498b694cee44cb37f7d197c78fc6eb4e7a11cda2f850129c6bed8a010e35a/diff:/var/snap/docker/common/var-lib-docker/overlay2/d81abc087044d2830b87a83bb45435f51899570b570ac794da1c3f9e358c1c1c/diff:/var/snap/docker/common/var-lib-docker/overlay2/bec4fca0e42e15e606fecdd064fa01e11e9d7698940556ab6268800bb4d4e6f9/diff:/var/snap/docker/common/var-lib-docker/overlay2/9b244abb878931e56837c63a500e0bb84ec34987ee439f11a8ab2804c762e443/diff:/var/snap/docker/common/var-lib-docker/overlay2/fbb6793436583bb678a78b6169c8e2cb0b27f0e0030241a083128bccc6717b3e/diff",
                "MergedDir": "/var/snap/docker/common/var-lib-docker/overlay2/708e10514532a0846a9747395790afb3365cc4472f77060752ca4b3262245d85/merged",
                "UpperDir": "/var/snap/docker/common/var-lib-docker/overlay2/708e10514532a0846a9747395790afb3365cc4472f77060752ca4b3262245d85/diff",
                "WorkDir": "/var/snap/docker/common/var-lib-docker/overlay2/708e10514532a0846a9747395790afb3365cc4472f77060752ca4b3262245d85/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:548a79621a426b4eb077c926eabac5a8620c454fb230640253e1b44dc7dd7562",
                "sha256:e7a1de2ac1c68c9a6b687c0838eaeab19516f3f0a9a9eb9e51fb8f4763b784ba",
                "sha256:441a215b0f3032fd19f92e902b750ab5fbb134e80d12c94f235edfe90f658a86",
                "sha256:d073a44569afe8f498cc91c4d0a99f78512480e56328ac563db23249f76a8972",
                "sha256:c7082532a7899ab842409301d745375aa418e64d47d902fc67075cd081291491",
                "sha256:ba2db5e5abb604d3bba3ea4f42f54f19eb6c4f12d6185a97cf68cffcc970600b",
                "sha256:ae591e0d0bd91f68797bd6a29767b093ad14bf4f93be4c20e3bc21a845f4ea6b",
                "sha256:c984e7ebf19acc8f45c4afda4b0247ea3e249462579dc368dc53ad6ad263dfc3"
            ]
        },
        "Metadata": {
            "LastTagTime": "2023-06-03T13:07:07.895456932+03:00"
        }
    }
]
```
 
  </details>


```sh
$ cat logs/log.txt
```

```
Copyright (c) 2015-2021 The ISC Authors
```
