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
- [ ] 터미널 기본 조작 및 폴더 구성
- [ ] 파일 및 디렉토리 권한 변경 실습
- [ ] Docker 설치 및 기본 데몬 점검
- [ ] 컨테이너 실행 실습 (hello-world, ubuntu)
- [ ] 커스텀 Dockerfile 기반 웹 서버 빌드 및 실행
- [ ] 포트 매핑 접속 확인
- [ ] 바인드 마운트 반영 검증
- [ ] Docker 볼륨 데이터 영속성 검증
- [ ] 트러블슈팅 작성 (2건 이상)

---

## 4. 수행 로그 및 검증

### 4.1 Git 설정 결과
```bash
(git config --list 
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
credential.https://dev.azure.com.usehttppath=true
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
core.ignorecase=true)
### 4.2 터미널 조작 로그
```bash
(PART 1에서 수행한 명령어 및 출력 결과 붙여넣기)
```User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
$ pwd ls -la
/c/Users/User/Documents/seugyeon

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
$ mkdir -p workspace/test_dir

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon (main)
$ cd workspace

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
$ touch test_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
$ echo "Hello Codyssey Workstation" > test_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
$ cat test_file.txt
Hello Codyssey Workstation

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
$ cp test_file.txt copy_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
$ mv copy_file.txt renamed_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
$ rm renamed_file.txt
### 4.3 권한 실습 로그
```bash
(PART 2에서 수행한 명령어 및 출력 결과 붙여넣기)
```User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
$ ls -l
total 1
drwxr-xr-x 1 User 197121  0 Nov  4 17:17 test_dir/
-rw-r--r-- 1 User 197121 27 Nov  4 17:19 test_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
$ chmod 644 test_file.txt

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
$ chmod 755 test_dir

User@DESKTOP-6RMVFJO UCRT64 ~/Documents/seugyeon/workspace (main)
$ ls -l
total 1
drwxr-xr-x 1 User 197121  0 Nov  4 17:17 test_dir/
-rw-r--r-- 1 User 197121 27 Nov  4 17:19 test_file.txt
