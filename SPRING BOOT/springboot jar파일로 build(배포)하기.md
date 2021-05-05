![image](https://user-images.githubusercontent.com/43662673/116778716-97a2ea80-aaae-11eb-92bf-d94c970f09f2.png)

Maven Build 기능을 사용해 해당 프로젝트를 배포한다.

프로젝트 오른쪽 버튼 클릭한 후, Run As -> Maven build를 선택한다.



![image](https://user-images.githubusercontent.com/43662673/116778754-d5a00e80-aaae-11eb-9ff8-1d65e5faa7b8.png)



아까 Maven build 밑에 있는 Run Configuration을 누르거나, maven build를 처음 실행했다면 위와 같은 화면이 나온다.

Goals에 package라고 써 준다. Profiles에는 pom.xml이 초기 셋팅일텐데, 빌드 했을 때 'The requested profile "pom.xml" could not be activated because it does not exist.' 라는 오류와 함께 빌드가 실패한다면 Profiles란을 지우면 된다고 한다.

**Run**을 눌러 빌드를 시작하면 콘솔에 빌드 과정이 나오고, 빌드가 완료되면 해당 프로젝트 경로의 target 폴더에 jar 파일이 생성된다.

![image](https://user-images.githubusercontent.com/43662673/116778839-6e368e80-aaaf-11eb-866a-4edb312ba1fd.png)



이제 jar 파일 테스트를 해 보자.

CMD를 켜서 해당 jar 파일이 있는 경로로 이동한다. 다음의 명령어로 jar 파일을 실행한다.

```
$ java -jar [jar 파일명]

ex. $ java -jar mongdok-0.0.1-SNAPSHOT.jar
```

![image](https://user-images.githubusercontent.com/43662673/116779187-b48bed80-aaaf-11eb-9996-90f848d0c889.png)



이렇게 실행 후 브라우저를 열고 테스트하면 정상적으로 잘 실행되는 것을 볼 수 있다.

![image](https://user-images.githubusercontent.com/43662673/116779206-deddab00-aaaf-11eb-9795-7316492bd5dd.png)