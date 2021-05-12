BackEnd에서 https로 설정 후 Postman에서는 응답할 수 없다고 나왔다.

![image](https://user-images.githubusercontent.com/43662673/116777087-56f3a300-aaa7-11eb-8d80-38253591b841.png)



그래서 postman에서 ssl, proxy 설정하는 방법을 알아보자.



![image](https://user-images.githubusercontent.com/43662673/116777108-8a363200-aaa7-11eb-99fe-305303061042.png)

오른쪽 위 Settings를 누른다.



General 탭에서 SSL certificate verification을 off 시켜버리면 ssl 인증을 하지 않는다. 여기까지만 해도 대부분은 작동한다.



![image](https://user-images.githubusercontent.com/43662673/116777162-f44ed700-aaa7-11eb-81a0-c70e0bec8dc3.png)



근데 내 postman에는 저게 없다...?! 예전에 저렇게 했었는데...?!

그래서 다운받으니 있다^^.. 

![image](https://user-images.githubusercontent.com/43662673/116777251-8eaf1a80-aaa8-11eb-9340-692d7096b55c.png)

이제는 APP에만 있는 기능인가보다..



![image](https://user-images.githubusercontent.com/43662673/116777641-d9c92d80-aaa8-11eb-9096-ed37c5141e47.png)

이제 잘 된다..!

fail은,,, 맞는 리턴값임 ㅎㅎ