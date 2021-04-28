#### Redis 이미지 설치

```
docker pull redis
```

![image](https://user-images.githubusercontent.com/43662673/116177171-4dd4a000-a74e-11eb-84ca-a874644679d8.png)



#### docker-compose 파일 생성

docker-compose 파일이 뭔지 모르겠다면? (설명하는 md로 이동)

```
version: '3.0'

services:
  redis1:
    image: redis
    command: redis-server --requirepass root --port 6379
    restart: always
    ports:
      - 6379:6379
```



#### docker-compose 파일 실행

1) 로컬 PC에서 위에서 생성한 docker-compose 파일 위치로 이동

![image](https://user-images.githubusercontent.com/43662673/116177871-8e80e900-a74f-11eb-841c-9d8836ff15c7.png)

![image](https://user-images.githubusercontent.com/43662673/116178014-cdaf3a00-a74f-11eb-81cb-5109889e978f.png)



2) docker-compose 실행

```
docker-compose -f docker-compose.yml up
```

![image](https://user-images.githubusercontent.com/43662673/116178095-eae40880-a74f-11eb-9210-a5e60fe0c662.png)



#### redis-cli 접속하여 명령어 실행

1) redis-cli 접속

```
redis-cli -p 6379
```

![image](https://user-images.githubusercontent.com/43662673/116178332-53cb8080-a750-11eb-866f-ba0dc3fb6840.png)

아까 그 경로에서 실행하긴 했는데,, 일단 실험해보니 아무데서나 저 명령어가 실행되긴 한다. (근데 이전에 redis를 윈도우에 깔아놨어서 그것 때문인지는 모르겠다....!)



2) 패스워드 입력 (입력해야 앞으로 redis 명령어 입력 가능)

```
auth root
```



3) 실행

```
keys *
```



정상적으로 실행된 것을 확인할 수 있다!