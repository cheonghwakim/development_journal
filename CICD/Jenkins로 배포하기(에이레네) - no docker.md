### Ubuntu에 Jenkins 설치

Jenkins도 웹서버니까 현재 Ubuntu에서 사용하는 포트를 확인해본다.

![image](https://user-images.githubusercontent.com/43662673/117262330-166f9d00-ae8c-11eb-8c0f-385ccc82c9da.png)
![image](https://user-images.githubusercontent.com/43662673/117262393-29826d00-ae8c-11eb-8821-c31d6425c1d1.png)

그리고 Jenkins는 java가 필요하다. java가 설치되어 있는지 버전을 확인한다.

![image](https://user-images.githubusercontent.com/43662673/117262913-b4636780-ae8c-11eb-8a1f-37549b3e586b.png)

Jenkins 설치를 위한 repository key를 추가한다.

```shell
$ wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
```

![image](https://user-images.githubusercontent.com/43662673/117263101-e5439c80-ae8c-11eb-97a5-3f6b913b14c5.png)

추가가 되었다면 위와 같이 OK가 뜬다.

이번엔 repository를 추가한다.

![image](https://user-images.githubusercontent.com/43662673/117263229-0ad0a600-ae8d-11eb-9359-cee68c50da9b.png)

이제 apt-get 업데이트 후 jenkins를 설치한다.

```shell
$ sudo apt-get update
$ sudo apt-get install jenkins
```

설치가 되었다면 Jenkins를 실행하기 전에 포트를 변경해준다.

포트 번경은 /etc/default/jenkins에서 한다.

```shell
$ sudo vim /etc/default/jenkins
```

![image](https://user-images.githubusercontent.com/43662673/117266087-da3e3b80-ae8f-11eb-9344-24eb269706c5.png)

파일 안에서 HTTP_PORT를 찾아 7070으로 변경한다. (나는 원래부터 7070이라 되어있다..)

systemctl을 이용해 jenkins를 실행한다.

```shell
$ sudo systemctl start jenkins
```

systemctl은 아무 메세지도 안 뜨므로 status로 상태를 확인한다.

```shell
$ sudo systemctl status jenkins
```

![image](https://user-images.githubusercontent.com/43662673/117266364-24bfb800-ae90-11eb-8bc7-a46e73d34ed6.png)

이제 브라우저를 열고 https://<서버 IP>:7070을 열어본다.

혹시 아래와 같이 Jenkins가 보이지 않는다면 sudo systemctl stop jenkins로 다시 시작해본다.

![image](https://user-images.githubusercontent.com/43662673/117266714-841dc800-ae90-11eb-8b00-29157466675c.png)

보안인증 같은 거라고 한다.

/var/lib/jenkins/secrets/initialAdminPassword 이 경로에 있는 password를 확인해서 입력하라고 한다.

```shell
$ sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

---

#### GitLab에서 Access Token 생성하기

GitLab의 **User Settings > Access Tokens**에서 생성할 수 있다.

Name과 Expires at을 입력하고 Scopes를 선택한다. 그리고 Create personal access token 버튼을 클릭하면 Access Token이 생성된다.

![image](https://user-images.githubusercontent.com/43662673/117268382-3013e300-ae92-11eb-933e-dc40e4f85669.png)

생성된 Access Token을 Jenkins에 등록해야 한다.

Jenkins > Credentials > global > adding some credentials로 클릭해서 들어간다.

Jenkins의 navigation에는 Jenkins > Credentials > System > Global credentials (unresticed) > Add Credentials로 되어 있다.

Kind에는 GitLab API token을 선택한다.

Scope에는 Global(Jenkins, nodes, items, all child items, etc)를 선택한다.

API token에 GitLab에서 생성한 Access token을 입력한다.

ID와 Description을 작성한 후 OK 버튼을 클릭한다.

![image](https://user-images.githubusercontent.com/43662673/117269348-2b036380-ae93-11eb-910e-85ede6d72f86.png)

경로가 조금 다르긴 하지만 어떻게든 갈 수 있다. (API token: rjHMjpcAwks_y6Sj6v-5)

소스코드 관리 탭에서 깃 정보를 저장한다.

![image](https://user-images.githubusercontent.com/43662673/117267616-7288f000-ae91-11eb-8785-35c2a8130c1b.png)

위와 같은 에러가 자꾸 떠서 credential,, 일단 제껴두고

**Jenkins 관리 > 시스템 설정**으로 들어가서 Publish over SSH에 ssh로 배포할 곳의 서버 정보를 입력한다. 추가 버튼과 고급 버튼 클릭

![image](https://user-images.githubusercontent.com/43662673/117271906-9e0dd980-ae95-11eb-8b66-522b7ffab5fb.png)

![image](https://user-images.githubusercontent.com/43662673/117272081-c85f9700-ae95-11eb-93f7-69122826d59a.png)

여기서 잠깐 ubuntu에서 key쌍을 생성해야 한다.

```shell
$ cd ~/.ssh
$ pwd
/home/ubuntu/.ssh
$ ssh-keygen -t rsa
# 생성된 key 확인
$ ls
authorized_keys id_rsa id_rsa.pub
```

![image](https://user-images.githubusercontent.com/43662673/117273144-cea24300-ae96-11eb-9924-2137355db3e3.png)

```shell
$ vim ~/.ssh/authorized_keys (or $ cat ~/.ssh/authorized_keys)
```

![image](https://user-images.githubusercontent.com/43662673/117273534-3062ad00-ae97-11eb-99d0-67c78f691442.png)

그 다음 Jenkins SSH Key 등록하기



- maven, gradle 설정

  젠킨스 설정 > Global Tool Configuration으로 이동

  ![image](https://user-images.githubusercontent.com/43662673/117274244-d9a9a300-ae97-11eb-839f-029b0f9473b6.png)

  ​