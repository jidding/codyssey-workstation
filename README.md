# 개발 워크스테이션 구축 미션

## 1. 프로젝트 개요
본 프로젝트는 특정 PC 환경에 종속되지 않고 누구나 동일하게 실행, 배포, 디버깅할 수 있는 재현 가능한 개발 워크스테이션 구축을 목표로 합니다. 터미널 CLI 조작, Docker 컨테이너화, Git/GitHub 버전 관리를 직접 수행하고 검증합니다.

## 2. 실행 환경
- OS: Windows 11 (WSL2 / Ubuntu)
- Shell: bash
- Docker: (docker --version 결과 작성)
- Git: (git --version 결과 작성)

## 3. 수행 항목 체크리스트
- [x] Git 사용자 정보 설정 및 기본 브랜치 설정
- [x] 터미널 기본 조작 및 폴더 구성
- [x] 파일 및 디렉토리 권한 변경 실습
- [x] Docker 설치 및 기본 데몬 점검
- [x] 컨테이너 실행 실습 (hello-world, ubuntu)
- [ ] 커스텀 Dockerfile 기반 웹 서버 빌드 및 실행
- [ ] 포트 매핑 접속 확인
- [ ] 바인드 마운트 반영 검증
- [ ] Docker 볼륨 데이터 영속성 검증
- [ ] 트러블슈팅 작성 (2건 이상)

---

## 4. 수행 로그 및 검증

### 4.1 Git 설정 결과
```bash
diff.astextplain.textconv=astextplain
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
http.sslbackend=schannel
core.autocrlf=true
core.fscache=true
core.symlinks=false
pull.rebase=false
credential.helper=manager
credential.[https://dev.azure.com.usehttppath](https://dev.azure.com.usehttppath)=true
init.defaultbranch=main
core.editor="C:\Users\User\AppData\Local\Programs\Microsoft VS Code\bin\code" --wait
user.name=jidding
user.email=jmk2146@naver.com
init.defaultbranch=main
core.repositoryformatversion=0
core.filemode=false
core.bare=false
core.logallrefupdates=true
core.symlinks=false
core.ignorecase=true
```

### 4.2 터미널 조작 로그
```bash
User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
\$ pwd
/c/Users/User/Documents/seugyeon

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
\$ ls -la
total 8
drwxr-xr-x 1 User 197121 0 Nov 4 17:15 .
drwxr-xr-x 1 User 197121 0 Nov 4 17:15 ..

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
\$ mkdir -p workspace/test_dir

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
\$ cd workspace

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
\$ touch test_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
\$ echo "Hello Codyssey Workstation" > test_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
\$ cat test_file.txt
Hello Codyssey Workstation

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
\$ cp test_file.txt copy_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
\$ mv copy_file.txt renamed_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
\$ rm renamed_file.txt
```

### 4.3 권한 실습 로그
```bash
User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
\$ ls -l
total 1
drwxr-xr-x 1 User 197121  0 Nov  4 17:17 test_dir/
-rw-r--r-- 1 User 197121 27 Nov  4 17:19 test_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
\$ chmod 644 test_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
\$ chmod 755 test_dir

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
\$ ls -l
total 1
drwxr-xr-x 1 User 197121  0 Nov  4 17:17 test_dir/
-rw-r--r-- 1 User 197121 27 Nov  4 17:19 test_file.txt
```
### 4.4 Docker 기본 운영 및 컨테이너 로그
'''bash
User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
$ docker --version
Docker version 29.9.2, build a82e528

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
$ docker info
Client:
 Version:    29.9.2
 Context:    desktop-linux
 Debug Mode: false
 Plugins:
  agent: Docker AI Agent Runner (Docker Inc.)
    Version:  v1.152.0
    Path:     C:\Users\User\.docker\cli-plugins\docker-agent.exe
  ai: Docker AI Agent - Ask Gordon (Docker Inc.)
    Version:  v1.33.0
    Path:     C:\Users\User\.docker\cli-plugins\docker-ai.exe
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.38.1
    Path:     C:\Users\User\.docker\cli-plugins\docker-buildx.exe
  compose: Docker Compose (Docker Inc.)
    Version:  v5.6.1
    Path:     C:\Users\User\.docker\cli-plugins\docker-compose.exe
  debug: Get a shell into any image or container (Docker Inc.)
    Version:  0.49.0
    Path:     C:\Users\User\.docker\cli-plugins\docker-debug.exe
  desktop: Docker Desktop commands (Docker Inc.)
    Version:  4.98.0
    Path:     C:\Users\User\.docker\cli-plugins\docker-desktop.exe
  dhi: CLI for managing Docker Hardened Images (Docker Inc.)
    Version:  v0.0.9
    Path:     C:\Users\User\.docker\cli-plugins\docker-dhi.exe
  extension: Manages Docker extensions (Docker Inc.)
    Version:  v0.2.32
    Path:     C:\Users\User\.docker\cli-plugins\docker-extension.exe
  init: Creates Docker-related starter files for your project (Docker Inc.)
    Version:  v1.4.1
    Path:     C:\Users\User\.docker\cli-plugins\docker-init.exe
  mcp: Docker MCP Plugin (Docker Inc.)
    Version:  v0.44.2
    Path:     C:\Users\User\.docker\cli-plugins\docker-mcp.exe
  model: Docker Model Runner (Docker Inc.)
    Version:  v1.2.9
    Path:     C:\Users\User\.docker\cli-plugins\docker-model.exe
  offload: Docker Offload (Docker Inc.)
    Version:  v0.7.35
    Path:     C:\Users\User\.docker\cli-plugins\docker-offload.exe
  pass: Docker Pass Secrets Manager Plugin (beta) (Docker Inc.)
    Version:  v0.3.2
    Path:     C:\Users\User\.docker\cli-plugins\docker-pass.exe
  sandbox: "docker sandbox" is deprecated, use Docker Sandboxes instead (Docker Inc.)
    Version:  v0.13.0
    Path:     C:\Users\User\.docker\cli-plugins\docker-sandbox.exe
  scout: Docker Scout (Docker Inc.)
    Version:  v1.27.0
    Path:     C:\Users\User\.docker\cli-plugins\docker-scout.exe

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 29.9.2
 Storage Driver: overlayfs
  driver-type: io.containerd.snapshotter.v1
 Logging Driver: local
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Discovered Devices:
  cdi: docker.com/gpu=webgpu
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 nvidia runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: b7a25261e029d68978bbf290df0a62fc819b3c51
 runc version: v1.5.2-0-g29dd3dc2
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.18.54.1-microsoft-standard-WSL2
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
 CPUs: 8
 Total Memory: 7.605GiB
 Name: docker-desktop
 ID: 43e3a177-d860-487a-a2d8-d2742da8aa1f
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 HTTP Proxy: http.docker.internal:3128
 HTTPS Proxy: http.docker.internal:3128
 No Proxy: hubproxy.docker.internal
 Labels:
  com.docker.desktop.address=npipe://\\.\pipe\docker_cli
 Experimental: false
 Insecure Registries:
  hubproxy.docker.internal:5555
  127.0.0.0/8
  ::1/128
 Live Restore Enabled: false
 Firewall Backend: iptables


User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
d5e71e642bf5: Download complete 
Digest: sha256:c567b231f65614688711a75f31518a064258a51d442117a3e771a3a8fdba78ef
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.    (amd64)
 3. The Docker daemon created a new container from that image which runsthe
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/


User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
$ docker run -it ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
f3f25b84a7d7: Pull complete 
edafa32f5d9e: Pull complete 
21594acc2d8b: Download complete 
Digest: sha256:6a06111c3b0a8600feadb270aec771dc239bf407b25625f93f44ab00e11f4d3c
Status: Downloaded newer image for ubuntu:latest
root@a7afb44276fb:/# ls -la
total 60
drwxr-xr-x   1 root root 4096 Nov  4 11:15 .
drwxr-xr-x   1 root root 4096 Nov  4 11:15 ..
-rwxr-xr-x   1 root root    0 Nov  4 11:15 .dockerenv
drwxr-xr-x   2 root root 4096 Oct 25 10:26 .rock
lrwxrwxrwx   1 root root    7 Apr 20  2026 bin -> usr/bin
drwxr-xr-x   2 root root 4096 Apr 20  2026 boot
drwxr-xr-x   5 root root  360 Nov  4 11:16 dev
drwxr-xr-x   1 root root 4096 Nov  4 11:15 etc
drwxr-xr-x   3 root root 4096 Oct 25 10:26 home
lrwxrwxrwx   1 root root    7 Apr 20  2026 lib -> usr/lib
lrwxrwxrwx   1 root root    9 Apr 20  2026 lib64 -> usr/lib64
drwxr-xr-x   2 root root 4096 Oct 25 10:25 media
drwxr-xr-x   2 root root 4096 Oct 25 10:25 mnt
drwxr-xr-x   2 root root 4096 Oct 25 10:25 opt
dr-xr-xr-x 171 root root    0 Nov  4 11:16 proc
drwx------   2 root root 4096 Oct 25 10:26 root
drwxr-xr-x   4 root root 4096 Oct 25 10:26 run
lrwxrwxrwx   1 root root    8 Apr 20  2026 sbin -> usr/sbin
drwxr-xr-x   2 root root 4096 Oct 25 10:25 srv
dr-xr-xr-x  12 root root    0 Nov  4 11:16 sys
drwxrwxrwt   2 root root 4096 Oct 25 10:25 tmp
drwxr-xr-x  12 root root 4096 Oct 25 10:24 usr
drwxr-xr-x  11 root root 4096 Oct 25 10:26 var
root@a7afb44276fb:/# echo "Hello inside Ubuntu Container"
Hello inside Ubuntu Container
root@a7afb44276fb:/# exit
exit

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
$ docker images
                                                    i Info →   U  In Use
IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest   c567b231f656       25.9kB         9.49kB    U   
ubuntu:latest        6a06111c3b0a        163MB         45.9MB    U   

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
$ docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS           PORTS     NAMES
a7afb44276fb   ubuntu        "bash"     11 minutes ago   Exited (0) 5 minutes ago             angry_agnesi
e0085fd59fc6   hello-world   "/hello"   13 minutes ago   Exited (0) 9 minutes ago             elated_carver
'''

---

## 5. 핵심 개념 정리
- **절대 경로 vs 상대 경로**: 
- **파일 권한 (rwx, 755, 644)**: 
- **포트 매핑의 필요성**: 
- **Docker 볼륨 (영속성)**: 
- **Git vs GitHub 차이**: 

---

## 6. 트러블슈팅
### 이슈 #1: 
- **문제**: 
- **원인 가설**: 
- **확인 과정**: 
- **해결 방법**: 

### 이슈 #2: 
- **문제**: 
- **원인 가설**: 
- **확인 과정**: 
- **해결 방법**: