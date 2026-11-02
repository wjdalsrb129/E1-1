# E1-1
내 컴퓨터에 개발자용 '작업실' 꾸미기

## 1. 프로젝트 개요(미션 목표 요약)
- 리눅스 CLI(터미널), Docker(컨테이너), Git/GitHub(버전 관리 및 협업) 도구들을 사용해여 개발 환경 구축 
- 이를 통해, 같은 서비스를 여러 번 실행해도 재현되는 환경을 만드는 사고방식을 경험하는 것이 목표
- 이후 리눅스 트러블슈팅, CI/CD 파이프라인, 클라우드 배포/운영 등으로 자연스럽게 확장

## 2. 실행 환경(OS/쉘/터미널, Docker 버전, Git 버전)
- OS: Ubuntu 26.04.1 LTS
- Shell: bash
- Docker: 29.9.2
- Git: 2.53.0
```
$ echo -e "OS: $(grep -oP '(?<=PRETTY_NAME=")[^"]+' /etc/os-release)\nShell: $(basename "$SHELL")\nDocker: $(docker --version | awk '{print $3}' | tr -d ',')\nGit: $(git --version | awk '{print $3}')"
OS: Ubuntu 26.04.1 LTS
Shell: bash
Docker: 29.9.2
Git: 2.53.0
```
- 검증 증거: [env 결과](./evidence/0.env_img/0.env.png)

## 3. 레포지터리 구조

## 4. 수행 항목 체크리스트(터미널/권한/Docker/Dockerfile/포트/볼륨/Git/GitHub)

| 분류 | 항목 | 검증 상세 | 
|---|---|---|
| 리눅스 CLI | [(1) 터미널 기본 조작](#1-터미널-기본-조작) | 현재 위치 확인, 목록 확인(숨김 파일 포함), 이동, 생성, 복사, 이동/이름변경, 삭제, 파일 내용 확인, 빈 파일 생성 |
| 리눅스 CLI | [(2) 파일 권한](#2-파일-권한) | 권한 확인/변경, 권한 변경 전/후 비교 |


### 1) 리눅스 CLI
터미널로 기본 적인 CLI 명령어를 수행하고, 파일의 권한을 변경 및 확인

#### (1) 터미널 기본 조작
<!-- 미널 조작 로그 기록: 명령어 + 출력 결과를 기술 문서에 기록한다. -->

- 검증 대상: **현재 위치 확인**
    - 검증 방법(명령어): `pwd`
    - 검증 결과(출력)
    ```
    $ pwd
    /home/ruav/mkj
    ```
    - 검증 증거: [`pwd` 결과](./evidence/1.terminal_img/1.pwd.png)

- 검증 대상: **목록 확인(숨김 파일 포함)**
    - 검증 방법(명령어): `ls -al`
    - 검증 결과(출력):
    ```
    $ ls -al
    total 24
    drwxr-xr-x 4 ruav ruav 4096 Nov  2 19:06 .
    drwxr-xr-x 3 ruav ruav 4096 Nov  2 18:55 ..
    drwxr-xr-x 7 ruav ruav 4096 Nov  2 18:55 .git
    -rw-r--r-- 1 ruav ruav 7386 Nov  2 20:06 README.md
    drwxr-xr-x 6 ruav ruav 4096 Nov  2 19:09 evidence
    ```
    - 검증 증거: [`ls -al` 결과](./evidence/1.terminal_img/2.ls-al.png)

- 검증 대상: **이동**
    - 검증 방법(명령어): `cd`
    - 검증 결과(출력):
    ```
    $ cd evidence
    ruav@DESKTOP-9HA9I8V:~/mkj/E1-1/evidence$
    ```
    - 검증 증거: [`cd` 결과](./evidence/1.terminal_img/3.cd.png)

- 검증 대상: **새폴더 생성**
    - 검증 방법(명령어): `mkdir`
    - 검증 결과(출력):
    ```
    $ mkdir new_dir
    $ ls
    README.md  evidence  new_dir
    ```
    - 검증 증거: [`mkdir` 결과](./evidence/1.terminal_img/4.mkdir.png)

- 검증 대상: **빈 파일 생성**
    - 검증 방법(명령어): `touch`
    - 검증 결과(출력):
    ```
    $ touch hello.txt
    $ cat hello.txt
    $ ls -al
    total 32
    drwxr-xr-x 5 ruav ruav 4096 Nov  2 20:37 .
    drwxr-xr-x 3 ruav ruav 4096 Nov  2 18:55 ..
    drwxr-xr-x 7 ruav ruav 4096 Nov  2 18:55 .git
    -rw-r--r-- 1 ruav ruav 9549 Nov  2 20:37 README.md
    drwxr-xr-x 6 ruav ruav 4096 Nov  2 20:30 evidence
    -rw-r--r-- 1 ruav ruav    0 Nov  2 20:37 hello.txt
    drwxr-xr-x 2 ruav ruav 4096 Nov  2 20:30 new_dir
    ```
    - 검증 증거: [`touch` 결과](./evidence/1.terminal_img/5.touch.png)


- 검증 대상: **파일 내용 확인**
    - 검증 방법(명령어): `cat`
    - 검증 결과(출력):
    ```
    $ cat hello.txt
    $ echo "Hello world!" > hello.txt
    $ cat hello.txt
    Hello world!

    $ echo "Welcome to Linux!" >> hello.txt
    $ cat hello.txt
    Hello world!
    Welcome to Linux!
    ```
    - 검증 증거: [`cat` 결과](./evidence/1.terminal_img/6.cat.png)

- 검증 대상: **복사**
    - 검증 방법(명령어): `cp`
    - 검증 결과(출력):
    ```
    $ cp hello.txt hello_copy.txt
    $ ls
    README.md  evidence  hello.txt  hello_copy.txt  new_dir    
    ```
    - 검증 증거: [`cp` 결과](./evidence/1.terminal_img/7.cp.png)

- 검증 대상: **이동/이름변경**
    - 검증 방법(명령어): `mv`
    - 검증 결과(출력):
    ```
    $ mv hello_copy.txt hello_copy_copy.txt
    $ ls
    README.md  evidence  hello.txt  hello_copy_copy.txt  new_dir    
    
    $ mv hello_copy_copy.txt new_dir/hello_copy_copy.txt
    $ cd new_dir/
    $ ls
    hello_copy_copy.txt
    ```
    - 검증 증거: [`mv` 결과](./evidence/1.terminal_img/8.mv.png)

- 검증 대상: **삭제**
    - 검증 방법(명령어): `rm`
    - 검증 결과(출력):
    ```
    $ ls
    hello_copy_copy.txt
    $ rm hello_copy_copy.txt 
    $ ls
    ```
    - 검증 증거: [`rm` 결과](./evidence/1.terminal_img/9.rm.png)

#### (2) 권한 실습 및 증거 기록
-->

#### (2) 파일 권한
<!-- 권한을 확인/변경하는 명령을 수행하고, 변경 전/후 비교를 기술 문서에 남긴다.
최소 요구: 파일 1개, 디렉토리 1개에 대해 권한 변경 실험을 수행한다. -->





### 2) Docker
- Docker를 설치 및 점검

#### Docker 설치 및 기본 점검
    Docker 버전 확인 결과를 기록한다. (docker --version)
    Docker 데몬 동작 여부 확인 결과를 기록한다. (docker info 또는 동등 점검)

docker --version, docker info 등 설치·점검 결과
docker images, docker ps -a, docker logs, docker stats 등 운영 명령 실행 흔적

#### Docker 기본 운영 명령 수행

이미지: 다운로드/목록 확인 (예: docker images)
컨테이너: 실행/중지/목록 확인 (예: docker ps, docker ps -a)
운영: 로그 확인 (예: docker logs), 리소스 확인 (예: docker stats)
수행 명령과 출력 결과를 기술 문서에 남긴다.

#### 컨테이너 실행 실습

hello-world 실행 성공을 기록한다.
ubuntu 컨테이너를 실행하고 내부 진입 후 간단 명령(예: ls, echo) 수행 결과를 기록한다.
컨테이너 종료/유지(attach/exec 등)의 차이를 스스로 관찰하고 간단히 정리한다.

- 컨테이너를 실행/관리
- 간단한 웹 서버를 Dockerfile로 컨테이너화
- 포트 매핑으로 접속을 확인
- 바인드 마운트/볼륨으로 "변경 반영"과 "데이터 영속성"을 직접 검증

#### 기존 Dockerfile 기반 커스텀 이미지 제작

아래 방식 중 하나를 선택하여 기존 Dockerfile/이미지 기반의 커스텀 이미지를 만든다.
(A) 웹 서버 베이스 이미지 활용(예: NGINX/Apache 등) + 정적 콘텐츠/설정만 교체
(B) Linux 베이스 이미지(예: ubuntu/alpine 등) + 기본 기능(패키지/사용자/환경변수/헬스체크 등) 추가
제작 결과는 아래 조건을 만족해야 한다.
커스텀 이미지 빌드 성공 및 컨테이너 실행 성공
기술 문서에 다음을 포함한다.
어떤 “기존 베이스(이미지/예시 Dockerfile)”를 선택했는지
내가 적용한 커스텀 포인트 각각의 목적(간단 요약)
빌드/실행 명령 + 핵심 결과(출력/스크린샷)

#### 포트 매핑 및 접속 증거
브라우저 접속 화면(또는 curl 응답)을 기술 문서에 첨부한다.

#### Docker 볼륨 영속성 검증
Docker 볼륨을 생성하고 컨테이너에 연결한다.
컨테이너 삭제 전/후로 데이터를 확인하여 데이터가 유지됨을 증명한다.
기술 문서에 생성/연결/검증 절차(명령+출력)를 포함한다.


실행 결과(로그/접속/데이터 유지)로 핵심 흐름을 확인

이미지와 컨테이너의 분리
격리된 실행 환경
포트·스토리지 연결 방식
&rarr; "왜 이런 설계가 필요한지"를 설명 가능한 형태로 정리

- Docker 운영/검증 로그
docker --version, docker info 등 설치·점검 결과
docker images, docker ps -a, docker logs, docker stats 등 운영 명령 실행 흔적
- Dockerfile 기반 웹 서버 컨테이너
웹 서버 소스코드(예: app/ 또는 src/)
Dockerfile
빌드/실행 명령 및 결과 로그(터미널 스크린샷 가능)
포트 매핑 접속 성공 증거(스크린샷 또는 로그)
- 포트 매핑 접속 증거
p <host_port>:<container_port>로 실행 후, 브라우저 접속 화면(주소창 포함)을 기술 문서에 첨부한다.
- 바인드 마운트 반영 + 볼륨 영속성 증거
바인드 마운트: 실행 명령 + 호스트 변경 전/후 비교
Docker 볼륨: 생성/연결/검증 명령 + 컨테이너 삭제 전/후 비교


### 3) Git/GitHub
- Git 설정 및 GitHub/VSCode 연동 증거

#### Git 설정 및 GitHub 연동
* Git 사용자 정보/기본 브랜치 설정을 완료하고 git config --list 결과를 기록한다.
* GitHub 로그인 및 저장소 연동을 완료하고, 연동 증거(스크린샷 등)를 기술 문서에 첨부한다.

## 검증 방법(어떤 명령으로 무엇을 확인했는지) + 결과 위치 링크
## 트러블슈팅 2건 이상(문제 → 원인 가설 → 확인 → 해결/대안)
## 기술 문서만 읽어도 전체 수행 내용을 파악할 수 있어야 한다.

## 과제 목표
절대 경로와 상대 경로의 차이를 예시를 들어 설명할 수 있다.
    절대 경로: 전체 경로를 모두 나열
    상대 경로: 현재 위치 기준으로 폴더 구조 표현 &rarr; 다른 환경에서 실행할 때 필요
파일 권한의 의미(r/w/x)와 755, 644 같은 표기가 어떤 규칙으로 해석되는지 설명할 수 있다.
기존 Dockerfile을 기반으로 “커스텀 이미지”를 만들 수 있다.
포트 매핑이 필요한 이유를 설명할 수 있다.
Docker 볼륨(영속 데이터)을 설명할 수 있다.
Git과 GitHub의 역할 차이(로컬 버전관리 vs 원격 협업 플랫폼)를 설명할 수 있다.



## 보너스 과제 (선택)
Docker Compose 기초
docker-compose.yml의 기본 구조를 학습하고, 단일 서비스를 Compose로 실행한다.
배움 포인트: 컨테이너 실행 명령이 “문서화된 실행 설정”으로 바뀌는 이유
Docker Compose 멀티 컨테이너
웹 서버 + (임의의 보조 서비스) 2개 이상을 Compose로 함께 실행한다.
컨테이너 간 네트워크 통신이 가능한지 확인한다.
배움 포인트: 네트워크/서비스 디스커버리 개념 맛보기
Compose 운영 명령어 습득
up, down, ps, logs를 사용해 실행/종료/상태/로그를 관리한다.
배움 포인트: 운영 관점의 “상태 확인 루틴” 만들기
환경 변수 활용
Dockerfile 또는 Compose에서 환경 변수를 주입해 서버 포트/모드를 바꿔본다.
배움 포인트: 설정과 코드의 분리
GitHub SSH 키 설정
HTTPS 대신 SSH로 푸시가 가능하도록 키를 등록하고 동작을 확인한다.
배움 포인트: 인증 방식 차이와 보안 습관