## git daemon 설정

#### git daemon?
- 블특정 다수에게 읽기 접근을 허용할 때 사용하는 Git 서버
- Git 프로토콜이 http 프로토콜보다 효율적이므로 속도가 빠름.
- git daemon으로 서버 생성 시 윈도우 환경(ex)git bash)에서 push 관련 작동 X
- 따라서 Ubuntu 설치(Microsoft store) 후 실행

##### git 설치

```cmd
sudo apt-get install git
```

##### git username, email

```cmd
git config --global user.name "유저이름"
git config --global user.email 메일주소
```

##### Repo 폴더 생성 이후 test.git 생성, test.git에서 명령

```cmd
git init --bare --shared 
```
- --bare : 워킹디렉토리가 없는 저장소, 어떤 서버를 설치하더라도 저장소를 Bare 저장소로 만들어야 함.
- --shared : 자동으로 그룹 쓰기 권한을 추가함

##### Repo의 상위폴더로 올라온 후 git protocol 활성화

```cmd
git daemon --reuseaddr --verbose --export-all --enable=receive-pack --base-path=`pwd`/Repo
```
- reuseaddr : 서버가 기존의 연결이 타임아웃될 때까지 기다리지 말고 바로 재시작하게 하는 옵션
- verbose : 저장소와 관련된 내용을 상세히 출력하는 옵션
- --enable=receive-pack : 이 옵션이 없는 경우 외부에서 push가 불가능
- base-path=폴더주소 : 사람들이 프로젝트를 Clone할 때 전체 경로를 사용하지 않아도 됨



이후 <b>git://ip주소/test.git</b> 으로 clone / remote 연결 후 push 가능 (in Ubuntu)
