Google Cloud Platform에서 프로젝트 생성 후 API 발급 받는 방법은 지난 'Unity와 Google Cloude TTS API 연결하기'와 같고, 나는 같은 프로젝트의 라이브러리에서 Cloud Speech-to-Text API 만 사용 누른뒤 TTS때 썼던 API Key를 그대로 사용했다.


![image](https://user-images.githubusercontent.com/43662673/115524565-408c6100-a2c9-11eb-8533-b1a17d591218.png)



REST 요청을 보내는 형식은 아래와 같다.

![image](https://user-images.githubusercontent.com/43662673/115524605-48e49c00-a2c9-11eb-9d92-d6ee48b55915.png)

https://cloud.google.com/speech-to-text/docs/basics

근데 이대로 했는데 에러를 반환했다.

알고보니 .WAV파일 형식은 encoding과 sampleRateHertz를 지정할 필요가 없었다. (아래 사진 설명)

![image](https://user-images.githubusercontent.com/43662673/115524648-53069a80-a2c9-11eb-9e28-9602a2a1a438.png)


https://cloud.google.com/speech-to-text/docs/encoding?hl=ko

그래서 config엔 languageCode만 넣으면 됐다.

```
string json = "{ \"config\": { \"languageCode\" : \"ko-KR\" }, \"audio\" : { \"content\" : \"" + file64 + "\"}}";
```
결과는 이렇게 transcript에 내가 한말이 글자로 출력된다 


![image](https://user-images.githubusercontent.com/43662673/115524691-5e59c600-a2c9-11eb-9379-f792e577e4a4.png)


앞으로 녹음버튼 클릭/정지 방식이 아니라, 스트리밍 방식도 하고싶다

https://cloud.google.com/speech-to-text/docs/streaming-recognize


+REST 요청 JSON부분에서, 

![image](https://user-images.githubusercontent.com/43662673/115524763-6ade1e80-a2c9-11eb-9ec1-1ccad67901b9.png)


https://cloud.google.com/speech-to-text/docs/quickstart-protocol?hl=ko

이렇게 enableWordTimeOffsets가 있는것도 있는데 이건 아니니까 혼동 주의..


참고링크

https://cloud.google.com/speech-to-text/docs/basics

https://cloud.google.com/speech-to-text/docs/quickstart-protocol?hl=ko

https://cloud.google.com/speech-to-text/docs/encoding?hl=ko

https://brunch.co.kr/@sunghyunlim/24
