### 설치방법

1. Apache JMeter 다운로드 페이지 접속

   https://jmeter.apache.org/download_jmeter.cgi

2. apache-jmeter-5.4.1.zip 클릭해서 다운로드 후 압축해제

   ![img](https://blog.kakaocdn.net/dn/kywuv/btq2hYz9kTX/5imZ8LkonnlugZ5b6nxJJ1/img.png)



### 실행방법

```shell
cmd -> 압축 푼 폴더 아래 bin 폴더로 이동 -> jmeter 입력 후 엔터
```

![image-20210525234430577](C:\Users\0901B\AppData\Roaming\Typora\typora-user-images\image-20210525234430577.png)

그럼 아래와 같은 GUI가 나온다. CLI는 아래 테스트 방법에서 언급할 예정

![image-20210525234522977](C:\Users\0901B\AppData\Roaming\Typora\typora-user-images\image-20210525234522977.png)



### 테스트

- **테스트 전 유의 사항**

  테스트 하는 웹 어플리케이션 서버와 테스트를 돌리는 서버는 서로 달라야 한다.

  **JMeter를 돌리는 서버와 웹 어플리케이션 서버가 같으면 같은 메모리를 사용하기 때문에 정확한 값을 측정할 수 없다!**



**JMeter 테스트 용어**

- Thread Group : 테스트에 사용될 쓰레드 개수, 쓰레드 1개당 사용자 1명

- Sampler : 사용자의 액션 (예: 로그인, 게시물 작성, 게시물 조회 등)

- Listener : 응답을 받아 리포팅, 검증, 그래프 등 다양한 처리

- Configuration : Sampler 또는 Listener가 사용할 설정 값 (쿠키, JDBC 커넥션 등)

- Assertion : 응답 확인 방법 (응답 코드, 본문 내용 비교 등)



#### 1. 테스트 생성하기

![img](https://blog.kakaocdn.net/dn/detGCA/btq2gCSqvjI/UBsqwcMygZrVAFoJ8FnjYk/img.png)



#### 2. Thread Group

테스트할 유저 수를 설정한다.

1에서 만든 테스트에 오른쪽 클릭 -> Add -> Threads (Users) -> Thread Group

![img](https://blog.kakaocdn.net/dn/bkO8wb/btq2hJJ5WsA/8rthB5UKaEgyrNPWE0PO8k/img.png)



![img](https://blog.kakaocdn.net/dn/bODj0u/btq2hIRZ620/QHICxTN8Jhky0nYq0WZTi0/img.png)



**Action to be taken after a Sampler error**

- Error가 리턴됐을 때 어떻게 할 건지에 대한 설정



**Thread Properties**

- Number of Threads : 쓰레드 개수
- Ramp-up period : 쓰레드 개수를 만드는데 소요되는 시간
- Loop Count : infinite | n 으로 값을 설정할 수 있으며 설정된 값에 따라 **Number of Threads X Ramp-up period** 만큼 요청을 다시 보낸다.



#### 3. Sampler

2에서 사용자를 만들었으니 이제 사용자가 해야 할 행동을 정의하자.

2에서 만든 Thread Group 우클릭 -> Add -> Sampler -> HTTP Request 클릭

![img](https://blog.kakaocdn.net/dn/bUwpee/btq2gDcMjM4/UTusAINKBEa80GRKKkROU0/img.png)



내가 만든 Controller에 요쳥을 보내는 Sampler를 만들자

![img](https://blog.kakaocdn.net/dn/E6Jhg/btq2hCRHb0a/kqhTRuEj1dwmLsM6nBm9Z1/img.png)

나 같은 경우는 밑과 같이 설정해 주었다.

![image](https://user-images.githubusercontent.com/43662673/119537034-9c647100-bdc4-11eb-85bd-7064258f8a78.png)

#### 4. Listener

3에서 만든 Sampler가 받아오는 리턴 값을 바탕으로 그래프, 레포팅을 만들어주는 Listener를 만든다.

3에서 만든 HTTP Request에 오른쪽 클릭 -> Add -> Listener -> View Results Tree, Summary Report, View Results in Table 생성

![img](https://blog.kakaocdn.net/dn/nLefX/btq2lqWPUiT/UrfciA11RX9lCVewFx2VP1/img.png)



#### 5. Assertion

응답값이 제대로 왔는지 검증하기 위해 Assertion을 추가한다.

3에서 만든 HTTP Request 우클릭 -> Add -> Assertions -> Response Assertion 클릭

![img](https://blog.kakaocdn.net/dn/bTBstW/btq2kBRUbYc/bhf8hYuIm5Zh4lwirPZ5x0/img.png)

![img](https://blog.kakaocdn.net/dn/m5eCs/btq2h3n6Ehq/flEEiO1VpoXb0KCIWvXXBK/img.png)

Text Response -> 맨 아래 Add -> 추가된 Patterns to Test 더블클릭 -> perfTest PostsId 입력



!! 근데 나 같은 경우는 result로 JSON이 오기 때문에 JSON Assertion을 추가한다.

![image-20210526015850822](C:\Users\0901B\AppData\Roaming\Typora\typora-user-images\image-20210526015850822.png)



Response Assertion처럼 하면 결과가 틀렸다고 뜸

JSON path는 https://octoperf.com/blog/2018/04/19/jmeter-assertions/#size-assertion 여길 참고



위의 5단계를 다 하면 아래와 같은 상태

![image](https://user-images.githubusercontent.com/43662673/119538400-0b8e9500-bdc6-11eb-8dbd-2301a4a00092.png)



### JMeter 테스트 실행

실행 버튼 클릭하면 설정대로 테스트가 진행됨

![img](https://blog.kakaocdn.net/dn/WkaQr/btq2gD4VCeD/4GV4gkmtFHXLskrubekY8K/img.png)



### JMeter 테스트 결과



1. **View Results Tree**

   요청을 보낸 개수만큼 요청의 결과가 나온다.

   ![image](https://user-images.githubusercontent.com/43662673/119538740-5f00e300-bdc6-11eb-84ef-550f2f03e07a.png)

   ![image](https://user-images.githubusercontent.com/43662673/119538688-51e3f400-bdc6-11eb-9f84-059963c6afc6.png)



Response data를 클릭해보면 아까 컨트롤러에서 보낸 값을 볼 수 있다.



2. **View Results in Table**

   

   View Results Tree를 Table 형식으로 보여준다. 데이터는 동일

   ![image](https://user-images.githubusercontent.com/43662673/119538866-7f30a200-bdc6-11eb-91ba-a5ae22b11ffc.png)



3. **Summary Report**

   \- Label : Sampler 명

   \- # Samples : 샘플 실행 수 (Number of Threads X Ramp-up period)

   \- Average : 평균 걸린 시간 (ms)

   \- Min : 최소

   \- Max : 최대

   \- Std. Dev. : 표준편차

   \- Error % : 에러율

   \- Throughput : 분당 처리량

   \- Received KB/sec : 초당 받은 데이터량

   \- Sent KB/sec : 초당 보낸 데이터량

   \- Avg. Bytes : 서버로부터 받은 데이터 평균

    

   View Results에 대한 통계를 나타낸다. 통계 정보가 필요한 경우 사용

   ![image](https://user-images.githubusercontent.com/43662673/119539066-bbfc9900-bdc6-11eb-8bdc-03c0b6007a76.png)



### 에러가 나는 경우 화면

![image](https://user-images.githubusercontent.com/43662673/119540121-03cff000-bdc8-11eb-947c-dcc557074184.png)
