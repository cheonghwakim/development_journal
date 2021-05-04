1. 프로젝트 clone

   ```
   $ git clone + [repository 주소]
   ```

2. clone한 repository로 이동해서 ./mvnw 통해 Maven build 시작

   ```
   $ cd [repository]
   // .mvnw가 보이는 위치에서 실행해야 함
   $ ./mvnw clean package 
   // 현재 디렉토리에 있는 mvnw 파일 이전 기록들을 clean하고 새로 package로 빌드함
   ```

   **여기서 마주친 에러 ./mvnw clean package permission denied**

   ![image](https://user-images.githubusercontent.com/43662673/116809296-38a9a800-ab78-11eb-8248-2cce232f9461.png)

   --> 해당 명령어의 수행 권한이 없어서 발생하는 에러

   **해결 방안**

   ```
   $ sudo chmod +x mvnw
   ```

   위의 명령어로 권한을 부여하면 된다.

   이제 빌드를 하는 데 또 에러가...?!

   ![image](https://user-images.githubusercontent.com/43662673/116809745-917a4000-ab7a-11eb-9675-1e9526133f65.png)

   정말 인터넷에 검색해도 아무런 정보도 없었는데 해결책은 정말 간단했다.

   ![image](https://user-images.githubusercontent.com/43662673/116810034-60027400-ab7c-11eb-83db-61fcfaa383ec.png)

   ```
   $ sudo su
   ```

   **sudo su** 명령어를 이용하여 root 계정으로 이동해야 함!!!

   그래도 에러가 난다면

   ![image](https://user-images.githubusercontent.com/43662673/116817510-ae763980-aba1-11eb-8980-8d83088caaaf.png)

   여기서 나온 것처럼 ~~/target/surefire-reports 폴더에 가서 생긴 문서를 보면 어디서 에러가 났는지 상세히 알려준다.

   ![image](https://user-images.githubusercontent.com/43662673/116817559-dc5b7e00-aba1-11eb-998a-e012e6a21d94.png)

   나 같은 경우는 Redis 연결 문제..!

   ㅜㅜ 해결했다,, port가 잘못 연결되어 있었다.. ㅜㅜ (감격)

   ​

3. ```BUILD SUCCESS``` 와 함께 다시 콘솔창이 뜨면 현재 디렉토리의 파일들 확인 후 target 폴더로 이동

   ```
   $ ls -al // target 폴더가 존재함
   $ cd target
   ```

4. 빌드된 jar 파일이 보이고 이를 실행함

   ```
   $ java - jar [빌드된 jar 파일 이름] &
   ```

   ​

## 코드 수정 후 재배포하기

1. 수정한 코드 다시 위의 repository에 커밋

2. ec2 콘솔에서 git pull 통해서 수정된 코드 가져오기

3. 현재 실행중인 프로세스 (서버) 종료

   - 현재 실행중인 프로세스 확인

     ```
     ps -ef | grep java 
     //결과 
     //실행환경 실행번호  .... 실행중인 프로세스 이름

     ```

   - 실행 번호를 통해서 특정 프로세스 죽이기

     ```
     kill -9 [프로세스의 실행번호]

     ```

   - 다시 실행 중 프로세스 확인 : 프로세스가 죽었는지 확인

     ```
     ps -ef | grep java

     ```

   - 간단 버전 프로세스 확인

     ```
     jps
     //결과 
     //실행번호 실행파일

     ```

4. 재배포

   ```
   ./mvnw clean package

   ```

5. 배포 확인 후 서버 실행

   ```
   ls -al 
   cd target
   java - jar [빌드된 jar 파일 이름] &

   ```

6. 웹 브라우저에서 `[ec2 ip 주소]:[포트번호]/[index 페이지 주소]` 를 통해서 확인