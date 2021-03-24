ubuntu에 기본으로 yum이 설치되어 있는 것 같으나 저번 플젝도 그렇고 이번 우리 서버에서도 yum이 없다..

![image](https://user-images.githubusercontent.com/43662673/112128641-f781b800-8c09-11eb-9f78-6644c3f5ea3e.png)



그래서  yum부터 설치하자

1. apt-get install yum
   ![image](https://user-images.githubusercontent.com/43662673/112129906-38c69780-8c0b-11eb-9dfb-283011d116fe.png)

   전에 해봤다.. 역시 안 된다.

2. yum-3.4.3.tar.gz 직접 다운받기

   2 - 1. wget을 이용하여 다운로드 한다.

   ![image](https://user-images.githubusercontent.com/43662673/112133768-5eee3680-8c0f-11eb-99ef-e9e1ce41ac2b.png)

   ```
   $ wget http://yum.baseurl.org/download/3.4/yum-3.4.3.tar.gz
   ```

   2 - 2. 확장자가 tar.gz이므로 tar을 이용하여 압축을 해제한다

   ```
   $ tar -xvzf yum-3.4.3-tar.gz
   ```

   2 - 3. 압축을 해제하면 폴더가 생성되므로, 해당 폴더로 이동

   ```
   $ cd yum-3.4.3
   ```

   -> 보통은 여기서 ./configure을 가서 make install을 하라고 해서 막힌다

   일단 이 상태에서도 인식을 못하는 건 마찬가지..

   ![image](https://user-images.githubusercontent.com/43662673/112131641-1afa3200-8c0d-11eb-980d-e663b48d9a0f.png)

   3 - 1. yum-3.4.3 폴더에 있는 yummain을 실행한다

   ```
   $ run ./yummain.py
   ```

   ![image](https://user-images.githubusercontent.com/43662673/112135205-e25c5780-8c10-11eb-8009-5bc47090f73e.png)

   안 되네...?



3. 이제부터는 sudo apt install yum이 가능하게 하기

   ![image](https://user-images.githubusercontent.com/43662673/112136254-0d937680-8c12-11eb-938b-5e826b0518b6.png)

   ubuntu version 확인

   ```
   $ lsb_release -a
   ```

   ![image](https://user-images.githubusercontent.com/43662673/112136610-872b6480-8c12-11eb-9e34-bd6874919ecb.png)

   

4. 미러사이트 건드리기!

   

   1) 일단 yum-3.4.3 폴더로 이동 -> etc/yum.repos.d 

   ![image](https://user-images.githubusercontent.com/43662673/112136841-dffafd00-8c12-11eb-9af4-19a719fd8789.png)

   yum.repos.d 파일이 없음 -> yum.conf 파일 건드려보기

![image-20210323204603821](C:\Users\0901B\AppData\Roaming\Typora\typora-user-images\image-20210323204603821.png)



### 21-03-24

결국 해결하지 못하고 다시 시도한다...!

저번에 해결하지 못했던 이유가 wget 으로 yum-3.4.3 버전을 다운 받아서인 것 같다...

그래서 혹시 몰라 yum-2.0.7 버전을 다시 다운받는다.

```
# wget http://yum.baseurl.org/download/2.0/yum-2.0.7.tar.gz
# tar -xvf yum-2.0.7.tar.gz
```

![image](https://user-images.githubusercontent.com/43662673/112240277-5f2c1780-8c8b-11eb-992a-a9ea5e599512.png)

![image](https://user-images.githubusercontent.com/43662673/112240302-6d7a3380-8c8b-11eb-888d-a87c4f6919a3.png)

이번에는 웬일인지 configure이 있다

![image](https://user-images.githubusercontent.com/43662673/112240417-9c90a500-8c8b-11eb-9d7c-13ed81b82a3a.png)

바로 실행

```
# ./configure
# make
# make install
```

만약 이렇게 해도 yum 명령어가 안 된다면

```
# apt-get install gettext
```

![image](https://user-images.githubusercontent.com/43662673/112240531-da8dc900-8c8b-11eb-9a3d-ca2eb5cfeca6.png)



그러면 새로운 에러가 뜬다!

![image-20210324103014262](C:\Users\0901B\AppData\Roaming\Typora\typora-user-images\image-20210324103014262.png)

^^

