1. GitLab에서 access Token 발급받기

   위의 메뉴에서 Settings로 이동

![image](https://user-images.githubusercontent.com/43662673/112259660-03be5180-8cac-11eb-8b01-e28372eec981.png)

2. 권한 설정 후 Create Personal access token을 누른다.

   ![image](https://user-images.githubusercontent.com/43662673/112259753-27819780-8cac-11eb-9821-475941c7d1e8.png)

3. 생성된 토큰 복사

   ![image-20210324142146668](C:\Users\0901B\AppData\Roaming\Typora\typora-user-images\image-20210324142146668.png)

4. Jenkins에서 GitLab 플러그인 설치

   ![image](https://user-images.githubusercontent.com/43662673/112260212-dcb44f80-8cac-11eb-8e8c-ea15af94b1c7.png)

   ![image](https://user-images.githubusercontent.com/43662673/112260745-de324780-8cad-11eb-83e1-1c4f6212ff97.png)

기달기달,,

못참아서 그냥 끔 ㅋㅋㅋㅋ

뭐 껐다 키니까... Installed에 잘 있다. --> GitLab 말고,,, GitLab API를 설치하쟈

![image](https://user-images.githubusercontent.com/43662673/112263079-0d4ab800-8cb2-11eb-823b-cae41ab02d11.png)

![image](https://user-images.githubusercontent.com/43662673/112263196-408d4700-8cb2-11eb-8497-dc7d217f6b1e.png)

(global)을 눌러 들어간다.

![image](https://user-images.githubusercontent.com/43662673/112263167-32d7c180-8cb2-11eb-8994-2d330befc968.png)

adding some credentials를 눌러 들어간다.

![image](https://user-images.githubusercontent.com/43662673/112263320-72061280-8cb2-11eb-8b6e-80671d7781dc.png)

아까 받은 토큰도 넣어주고 OK

![image](https://user-images.githubusercontent.com/43662673/112263474-b5608100-8cb2-11eb-9623-771113cb7cf0.png)

new Item을 눌러준다.

![image](https://user-images.githubusercontent.com/43662673/112275212-b4cfe680-8cc2-11eb-8394-61a584f4af5c.png)



---

다시



![image-20210324211032561](C:\Users\0901B\AppData\Roaming\Typora\typora-user-images\image-20210324211032561.png)

![image](https://user-images.githubusercontent.com/43662673/112309886-418c9b80-8ce7-11eb-94a3-7172fadd2d8c.png)

요건 에러~

![image](https://user-images.githubusercontent.com/43662673/112309932-52d5a800-8ce7-11eb-9ce7-a7347fb9b0bc.png)

요건 성공~

![image](https://user-images.githubusercontent.com/43662673/112310016-6bde5900-8ce7-11eb-9822-f39cd164effd.png)

jenkins에 GitLab에 연동할 User 생성해야 함

![image](https://user-images.githubusercontent.com/43662673/112311006-8e24a680-8ce8-11eb-916e-409aa2aa47e5.png)

메뉴에서 New Item 눌러주고

![image](https://user-images.githubusercontent.com/43662673/112310879-68979d00-8ce8-11eb-9378-914545bab4c3.png)

여기서 파란색으로 스크랩한 부분이 webhook url이다.



다음으로 GitLab에서 webhook 등록해야 한다.

![img](https://tech.osci.kr/assets/images/86039236/9.png)

1. ID/Password 방식

![img](https://tech.osci.kr/assets/images/86039236/10.png)

2. Secret Token 방식

   다시 build Trigger에 가서 고급 버튼을 눌러주면

   ![image](https://user-images.githubusercontent.com/43662673/112311887-887b9080-8ce9-11eb-8035-0dc5f31103fb.png)

   위와 같이 발급 받을 수 있다.

   ![image](https://user-images.githubusercontent.com/43662673/112312207-e6a87380-8ce9-11eb-803a-fc9e4b8ca675.png)

   Test로 push events를 눌러보면

   ![image](https://user-images.githubusercontent.com/43662673/112312156-d98b8480-8ce9-11eb-9d47-671db187c972.png)

   위와 같이 잘 실행되는 것을 볼 수 있다.

찐찐