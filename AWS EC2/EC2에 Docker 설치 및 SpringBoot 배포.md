> Docker 설치 및 데이터 가져오기

EC2에 올려진 서버에서 기존에 사용하던 DB와 연동 시키려면 EC2에도 DOCKER 설치가 필요하다.

### **1. Docker image push**

Docker에 계정을 만들고 원격저장소에 image를 push한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4fee6bc8-7272-4eb1-819e-fb894f757bc9/image-20210131195300520.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4fee6bc8-7272-4eb1-819e-fb894f757bc9/image-20210131195300520.png)

### **2. EC2 접속**

해당위치에 pem 파일 갖다놓기

```
ssh -i I4A308T.pem ubuntu@i4a308.p.ssafy.io
```

### **3. EC2에 Docker설치**

설치를 위해 사전에 해주어야 하는것들(아직 의미를 모르고 따라만..)

```
$sudo apt install apt-transport-https
$sudo apt install ca-certificates
$sudo apt install curl
$sudo apt install software-properties-common
```

Docker 설치

```
$curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

$sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

$sudo apt update

$apt-cache policy docker-ce

$sudo apt install docker-ce
```

### **4. Docker 이미지 PULL하기**

1번에서 push한 이미지를 불러온다.

```
$ sudo docker pull yj96/mariadb
```

> SpringBoot EC2에서 빌드하기

참고 : [https://victorydntmd.tistory.com/338](https://victorydntmd.tistory.com/338)

### **1. git clone하기**

```
$ git clone https://lab.ssafy.com/s04-webmobile1-sub3/s04p13a308.git
```

### **2. BackEnd 폴더로 이동**

```
$ cd s04p13a308/BackEnd
```

### **3. 빌드**

그 전에 빌드하기 위해서는 실행권한이 있어야 하므로, 권한을 수정해준다.

```
$ sudo chmod 777 ./mvnw

$ ll ./mvnw

$ ./mvnw clean package 
//현재 디렉토리에 있는 mvnw 파일을 이전 기록들을 clean 하고 새로 package로 빌드함

```

빌드파일은 target폴더에 생성된다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eac34c9a-d13b-435f-9a3a-b5d4b51dadf5/image-20210131200802107.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eac34c9a-d13b-435f-9a3a-b5d4b51dadf5/image-20210131200802107.png)

```
$ cd target

//서버가 닫혀있을때는 이 명령어로 실행하면 된다.
$ java -jar webBlog-0.0.1-SNAPSHOT.jar
```

끄읕~

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79bbc6c8-f971-4074-98ec-3ea4bfd74717/image-20210131203032143.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79bbc6c8-f971-4074-98ec-3ea4bfd74717/image-20210131203032143.png)

> SpringBoot EC2에서 배포하기

폴더 하나 생성하서 JAR 파일 복사

```jsx
cp s04p13a308/BackEnd/target/*.jar build/

//배포 터미널 꺼도 돌아감
nohup java -jar ~/build/webBlog-0.0.1-SNAPSHOT.jar &
```

주소창에는 localhost 대신에 i4a308.p.ssafy.io 써주면 됨

//s3config 파일 따로 보내기( 로컬-> ec2)

```jsx

scp -i "I4A308T.pem" S3Config.java ubuntu@i4a308.p.ssafy.io:~/s04p13a308/BackEnd/src/main/java/com/web/commitment/config/

scp -i "I4A308T.pem" CommitController.java [ubuntu@i4a308.p.ssafy.io](mailto:ubuntu@i4a308.p.ssafy.io):~/s04p13a308/BackEnd/src/main/java/com/web/commitment/controller/

scp -i "I4A308T.pem" UserController.java [ubuntu@i4a308.p.ssafy.io](mailto:ubuntu@i4a308.p.ssafy.io):~/s04p13a308/BackEnd/src/main/java/com/web/commitment/controller/
```

mysql -u root -p
