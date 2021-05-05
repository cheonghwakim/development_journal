다운로드 URL : [https://](https://github.com/microsoftarchive/redis)[github.com](https://github.com/microsoftarchive/redis)[/](https://github.com/microsoftarchive/redis)[microsoftarchive](https://github.com/microsoftarchive/redis)[/](https://github.com/microsoftarchive/redis)[redis](https://github.com/microsoftarchive/redis)

 

1. 다운로드 URL 의 하단에 release page 를 클릭해서 이동합니다.

![img](https://blog.kakaocdn.net/dn/c6gLd7/btqCuYzbtZp/q2Z6G7MHZdzWh63o0z6HKK/img.png)

![img](https://blog.kakaocdn.net/dn/sUV13/btqCz5i6guF/5AkZJXw3KmrX1mQG8tnCh1/img.png)

 

2. "3.2.100" 을 클릭합니다.

 

![img](https://blog.kakaocdn.net/dn/LcKO3/btqCxPuPfNY/KPRBUVsXAyHcVTBzM4Hig1/img.png)

 

3. "Redis-x64-3.2.100.msi" 를 클릭합니다.

![img](https://blog.kakaocdn.net/dn/bBsCMB/btqCymlEcvV/mDKiNtT3kzR9sqMnvfgQZK/img.png)

4. 다운로드 받은 파일을 실행하면 설치가 진행됩니다.

\- Next 신공을 이용해 그대로 진행합니다.

![img](https://blog.kakaocdn.net/dn/tJltP/btqCwWHGsa3/Z2QpTBEGHXfCUkBMOBcJ41/img.png)

![img](https://blog.kakaocdn.net/dn/tTopN/btqCwYrYYqQ/azMwkoDMzWRpV8x1kPirJk/img.png)

![img](https://blog.kakaocdn.net/dn/bFbxDR/btqCymlEdmp/NihKRwdOewOpl1VSP5StN0/img.png)

![img](https://blog.kakaocdn.net/dn/cbMihL/btqCz6oMdxQ/WqIwUy9M7SZaYPeMSGLIsk/img.png)

 

![img](https://blog.kakaocdn.net/dn/uF38e/btqCxPavQo5/YmzuexFDGrwUmzMfldneV1/img.png)

 

![img](https://blog.kakaocdn.net/dn/cXWctT/btqCuZLD3vH/dPNdLJLKz5O1Bn517OZp1k/img.png)

![img](https://blog.kakaocdn.net/dn/U5ELS/btqCymFRvaC/50vhkjzqtrxImFD8icD61K/img.png)

![img](https://blog.kakaocdn.net/dn/oZ50x/btqCymlEdAq/D7uBAZ2Q3gYDM0a0aAfq60/img.png)



5. 설치 확인 방법

   ```
   $ netstat -an|findstr 6379
   ```

   ![image](https://user-images.githubusercontent.com/43662673/116176489-30530680-a74d-11eb-87a4-d6352f2e8338.png)

   ```
   $ redis-cli
   ```

   ![image](https://user-images.githubusercontent.com/43662673/116176562-4eb90200-a74d-11eb-8c5e-f1774b18abd0.png)

   ....?!



​	ㅋ.. 멍충,,

![image](https://user-images.githubusercontent.com/43662673/116176617-65f7ef80-a74d-11eb-96b2-3ea45f216153.png)

​	Redis 설치된 곳으로 가서 치면 완료!