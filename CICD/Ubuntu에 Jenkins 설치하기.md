먼저 젠킨스도 웹서버이기 때문에 현재 Ubuntu에서 사용하는 포트를 확인한다.

포트확인 위해 nmap을 설치한다.

```
$ sudo apt-get install nmap
$ nmap localhost
```

![image](https://user-images.githubusercontent.com/43662673/112255119-f5b90280-8ca4-11eb-9b67-915ad8294efc.png)

8080포트를 사용하고 있지 않지만,, 혹시 모르니까 7070 포트를 사용하기로 한다.

그리고 Jenkins는 java가 필요하기 때문에 java가 설치되어 있는지 버전을 확인한다.

![image](https://user-images.githubusercontent.com/43662673/112255210-1f722980-8ca5-11eb-99b6-9c08da356878.png)



Jenkins 설치를 위한 repository key를 추가한다.

```
$ wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
```

![image](https://user-images.githubusercontent.com/43662673/112255325-47fa2380-8ca5-11eb-81e7-30dd5d166364.png)

추가가 되면 OK 메세지가 뜬다.

이번에는 repository를 추가한다.

![image](https://user-images.githubusercontent.com/43662673/112255375-65c78880-8ca5-11eb-8dbe-befafeb6443d.png)

이제 apt-get 업데이트 후 jenkins를 설치합니다.

```
$ sudo apt-get update
```

![image](https://user-images.githubusercontent.com/43662673/112255528-b9d26d00-8ca5-11eb-9b9c-cef5c199960d.png)

그런데 GPG error 가 나서 업데이트에 실패

```
W: GPG error: https://pkg.jenkins.io/debian-stable binary/ Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY <16개의 대문자 알파벳>
```

그럴 때는 

```
$ sudo apt-key adv --keyserver  keyserver.ubuntu.com --recv-keys <아까 그 16개 대문자 알파벳>
```

로 해결할 수 있다.

![image](https://user-images.githubusercontent.com/43662673/112255604-e1293a00-8ca5-11eb-891c-2fdf919bedc5.png)



다시 apt-get update를 하자.

![image](https://user-images.githubusercontent.com/43662673/112255671-05851680-8ca6-11eb-9233-9049e0f266d3.png)

성공!

그 다음

```
$ sudo apt-get install jenkins
```

설치가 되면 Jenkins 실행하기 전에 포트를 변경한다.

포트 변경은 /etc/default/jenkins에서 한다.

```
$ sudo vim /etc/default/jenkins 
```

파일 안에서 HTTP_PORT를 찾아 7070으로 변경한다.

```
# port for HTTP connector (default 8080; disable with -1)
HTTP_PORT=7070
```

systemctl을 이용해 jenkins를 실행한다.

```
$ sudo systemctl start jenkins
```

systemctl은 아무런 메시지가 나오지 않습니다. 그래서 status로 상태를 확인해 봐야 한다.

```
$ sudo systemctl status jenkins
```

![image](https://user-images.githubusercontent.com/43662673/112257172-c5bf2e80-8ca7-11eb-9c61-464a7a105968.png)



이제 브라우저를 열고 http://j4a401.p.ssafy.io:7070 에 들어간다.

만약 아래와 같이 젠킨스 화면이 보이지 않는다면

![image](https://user-images.githubusercontent.com/43662673/112257479-42eaa380-8ca8-11eb-94ba-a0d7a7bad7b5.png)

```
$ sudo systemctl stop jenkins
$ sudo systemctl start jenkins
```

중지했다가 다시 시작하면 보인다.



/var/lib/jenkins/secrets/initialAdminPassword 이 경로에 있는 password를 확인해서 입력하라고 하니 뭐가 써있는지 보러 간다. (보안인증같은 거라고 한다.)

![image](https://user-images.githubusercontent.com/43662673/112257761-aaa0ee80-8ca8-11eb-8bb7-52494639fe36.png)



추천하는 플러그인 설치하고

![image](https://user-images.githubusercontent.com/43662673/112257788-b7254700-8ca8-11eb-99ec-3e285c43790f.png)

플러그인 설치 중

![image](https://user-images.githubusercontent.com/43662673/112257831-c7d5bd00-8ca8-11eb-8964-6f6ade500372.png)

플러그인 설치 끝나고 유저 생성 화면이보임 -> 자주 사용하는 계정과 비번을 입력

![image](https://user-images.githubusercontent.com/43662673/112258772-66165280-8caa-11eb-8a6f-dade321c27a9.png)

![image](https://user-images.githubusercontent.com/43662673/112258886-a1b11c80-8caa-11eb-92a5-7a586a0871bf.png)

끄읏