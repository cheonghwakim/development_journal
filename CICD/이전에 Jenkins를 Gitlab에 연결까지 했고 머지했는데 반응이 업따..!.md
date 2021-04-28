이전에 Jenkins를 Gitlab에 연결까지 했고 머지했는데 반응이 업따..!

분명 build history에도 찍혔고

![image](https://user-images.githubusercontent.com/43662673/112315380-6f74de80-8ced-11eb-8b19-2fff82455d3b.png)

근데 바뀐 게 없단다...

![image](https://user-images.githubusercontent.com/43662673/112315421-7a2f7380-8ced-11eb-8fb7-6d8eb00684a9.png)



알고보니.,, 푸시할 때마다 shell을 수행하는 걸 넣어야 됐다...!

![image](https://user-images.githubusercontent.com/43662673/112315034-0beab100-8ced-11eb-82f1-3a28ad0631fd.png)

![image](https://user-images.githubusercontent.com/43662673/112315227-45bbb780-8ced-11eb-96e0-b498695f8dc8.png)



근데 저거 넣으니까 왜 자꾸 빌드 실패하는거지,,,?

Console Output을 보니까 경로가 home 디렉토리가 아니었다..

![image](https://user-images.githubusercontent.com/43662673/112316476-7c460200-8cee-11eb-9094-0632b5ab85f8.png)



경로 바꿔주니까 또 에러가,,

![image-20210324221636303](C:\Users\0901B\AppData\Roaming\Typora\typora-user-images\image-20210324221636303.png)



### SSH Key 생성해서 비밀번호 없이 pull하기

ubuntu에서 비밀번호 없이 pull할 수 있게 하자

![image](https://user-images.githubusercontent.com/43662673/112318932-e8c20080-8cf0-11eb-96b3-84f8e2a604b5.png)

id_rsa.pub이 있으면 ssh가 있는 것

https://goddaehee.tistory.com/254 여기 참고



근데 결국 https://webisfree.com/2017-05-19/git-%EC%95%84%EC%9D%B4%EB%94%94-%ED%8C%A8%EC%8A%A4%EC%9B%8C%EB%93%9C-%EC%9E%85%EB%A0%A5-%EC%95%88%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95 이걸로 해결..