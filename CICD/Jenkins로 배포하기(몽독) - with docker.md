1. 프로젝트 추가

   New Item --> 프로젝트 이름을 넣고 Freestyle project 를 선택하고 OK를 눌러준다.

   ![image](https://user-images.githubusercontent.com/43662673/116805582-64ba2e80-ab62-11eb-821b-37e5605275b7.png)

2. credential로 자신의 깃랩 아이디 비밀번호 입력

   ![image](https://user-images.githubusercontent.com/43662673/116805804-c333dc80-ab63-11eb-818f-46e4aaaa3c1d.png)

   ​

3. 소스 코드 관리 탭에서 깃 정보 저장

   ![image](https://user-images.githubusercontent.com/43662673/116805780-a4354a80-ab63-11eb-935c-652dfb43ebdc.png)



4. Build 탭으로 내려와서, 먼저 빌드 전에 컨테이너 stop![image](https://user-images.githubusercontent.com/43662673/116805963-0773ac80-ab65-11eb-97f8-0053c8a9b57a.png)

   ![image](https://user-images.githubusercontent.com/43662673/116806194-5bcb5c00-ab66-11eb-8fe9-3265cc709271.png)

   [근데 일단 저 mongdok_login이 뭘 뜻하는 건지 몰라서,, 나중에 추가할 예정]



5. Add build step을 클릭하고 Invoke top-level Maven targets를 선택한다.

   ![image](https://user-images.githubusercontent.com/43662673/116806231-96cd8f80-ab66-11eb-9fd4-4941ae9bf567.png)

   Maven clean과 install  설정을 해준다. pom.xml의 위치도 지정해줘야 함

   ![image](https://user-images.githubusercontent.com/43662673/116806352-50c4fb80-ab67-11eb-8417-e4fa988c8209.png)

6. send files or execute command over ssh 도 추가![image](https://user-images.githubusercontent.com/43662673/116808140-30e70500-ab72-11eb-91e4-11bbf29dcff5.png)

   **Source files:** 내가 전송할 파일의 위치를 적는다. 젠킨스의 workspace(var/jenkins/workspace) 기준으로 적게 되는데 git pull 로 당겨 온 스프링 부트 앱의 루트 경로라고 생각해도 된다. 그렇게 되면 (gradle build 시) jar 파일의 위치는 build/libs 안에 들어가 있다. 그 곳에 jar 파일이라고 명시를 해준다.

   **Remote Directory:** 파일을 전송할 원격 서버의 디렉터리를 명시하는 부분이다. 이 부분에서 조심해야 할게 아까 젠킨스의 서버 친구 맺기에서 설정한 폴더 기준으로 적어야 한다. 그 쪽에서 /home/ubuntu 라고 적어줬기 때문에 그 밑의 경로를 적는다. 사진에서는 /jenkins/deploy 라고 되어 있다. deploy라는 폴더는 jar 파일을 넣어놓기 위한 폴더로 사용하려고 만들어 놓았다. 미리 서버에 들어가서 저 폴더를 만들어 놓자.(이미 만들어 놓음)

   ```bash
   ubuntu/home/jenkins
   	ㄴdeploy(jenkins workspace에서 생성된 jar파일 여기로복사됨)
   	ㄴscript(sh 파일 넣을곳)
   ```


7. shell 두개 추가해서 docker  기존 컨테이너 삭제하고 다시 생성하는 명령어 작성

   ![image](https://user-images.githubusercontent.com/43662673/116819367-ca320d80-abaa-11eb-9155-2320428da5be.png)

   ![image](https://user-images.githubusercontent.com/43662673/116819386-de760a80-abaa-11eb-84b2-1977bae9c3e3.png)

   ​

#### [5. 깃랩과 연결된 젠킨스의 ec2 디렉토리에 springboot 서버에 대한 dockerfile 생성]

1. dockerfile 생성

   자신의 .docker 포트번호, jarfile 이름 넣기

   ```bash
   # Start with a base image containing Java runtime
   FROM java:8

   # Add Author info
   LABEL maintainer="asder36@naver.com"

   # Add a volume to /tmp
   VOLUME /tmp

   # Make port 8080 available to the world outside this container
   EXPOSE 8080

   # The application's jar file
   ARG JAR_FILE=target/MongdokLogin-0.0.1-SNAPSHOT.jar

   # Add the application's jar to the container
   ADD ${JAR_FILE} mongdok_loginAPI.jar

   # Run the jar file
   ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/mongdok_loginAPI.jar"]
   ```

   ![image](https://user-images.githubusercontent.com/43662673/116819648-e71b1080-abab-11eb-9ae4-6162bed6c2a8.png)

   프로젝트의 최상단에 Dockerfile 생성


여기까지 했으면 Build Now 눌러보기!

근데,,, 빌드가 안 됨..

![image](https://user-images.githubusercontent.com/43662673/117258604-19688e80-ae88-11eb-8ad7-5e3ec71308b0.png)

그럴 땐 Console Output을 보면 어디서 문제를 일으켰는지 볼 수 있음



#### webhook 설정을 통해 push 이벤트 발생시 빌드 자동화

Build Triggers에서

![Untitled 24](https://user-images.githubusercontent.com/43662673/117259559-2043d100-ae89-11eb-8c20-15832d947aa7.png)

옆에 나온 url이 깃랩에 써줄 url

고급 눌러서 토큰 generate, master 브랜치를 선택

![Untitled 25](https://user-images.githubusercontent.com/43662673/117259521-15893c00-ae89-11eb-8446-4c0518560490.png)

![Untitled 26](https://user-images.githubusercontent.com/43662673/117259585-26d24880-ae89-11eb-822f-368795bc8f33.png)

위에 url이랑 generate한 토큰 넣고 add

push event 눌러서

![Untitled 27](https://user-images.githubusercontent.com/43662673/117259582-25a11b80-ae89-11eb-9be4-4eaccc787497.png)

![Untitled 28](https://user-images.githubusercontent.com/43662673/117259584-26d24880-ae89-11eb-9910-133b6850ec44.png)

200 뜨면 성공