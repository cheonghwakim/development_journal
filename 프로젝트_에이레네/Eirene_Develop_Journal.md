# 개발 일지 🐱‍👓

> 청화 개발 일지 

<br>

### 2021-03-10

- 색깔별 맵 컨셉 정하기

  | 색깔        | 의미                                                         |
  | ----------- | ------------------------------------------------------------ |
  | 빨강        | 노을 지는 컨셉 (일을 마치고 집에 돌아오는 길 노을이 지고 있는 느낌) |
  | 주황        | 단풍으로 물들어 있는 길을 걷는 (가을의 맑은 하늘을 보여주기 → 경쾌 낙천) |
  | 노랑        | 황금빛 건물이나 사막 (사막은 약간 황폐한 느낌이 있을 수도 있으니까 황금빛 건물 안을 탐험하는 느낌...) |
  | 초록        | 오솔길 걸으면서 식물들과 소통하는 느낌 (피톤치드~)           |
  | 파랑        | 바다, 섬에서 길 따라가면서 ~~ (조약돌, 불가사리 같은 거랑 상호작용) 아니면 배 타고 다니면서 |
  | 진청        | 보름달 뜬 밤, 평화로운 느낌                                  |
  | 보라        | 보랏빛 숲 속 탐험  (몽환적인 느낌)                           |
  | 자주 (핑크) |                                                              |

  

- 회의중

빨강 - 크리스마스 방, 난로 

노랑 - 황금빛 건물

파랑 - 난파선 보물상자, 열쇠 

진청 - 배타고 반딧불이



### 2021-03-11

SubPJT1 하면서 생긴 에러

1.  raise RuntimeError(message)

해결 방법:

```
File "/home/gerald/miniconda3/envs/maskrcnn_benchmark/lib/python3.8/site-packages/torch/utils/cpp_extension.py", line 1413, in _run_ninja_build
raise RuntimeError(message)
RuntimeError: Error compiling objects for extension

이 에러가 떴을 때: 현재 설치되어있는 CUDA와 맞지않은 pytorch 패키지가 설치되어 있어서 생긴 문제

1) 현재 설치되어있는 cuda 버전과 맞는 pytorch 패키지를 설치
conda install pytorch torchvision cudatoolkit=11.2 -c pytorch

conda install pytorch torchvision cudatoolkit=10.0 -c pytorch

2) 만약 image_captioning.py를 실행할 때 DLL load failed가 뜬다면
환경 변수에 'C:\ProgramData\Anaconda3\Library\bin' 를 추가해준다

만약 그래도 안 되면 Intel-openmp을 설치해본다.. 참고: https://mclearninglab.tistory.com/30
```

2. DLL load failed : 지정된 모듈이 ~ 

해결방법:

```
CuDNN 버전, pytorch 버전, cuda 버전을 맞춰야 함
```



### 2021-03-12

```
logging 사용하기

사용하는 이유: 
	- 파이썬 프로그램에서 발생한 로그를 파일로 기록한다.
	- 매일 새로운 파일이 생성되며, 생성날짜를 파일명에 넣고 싶다.

사용 방법: 
	1) logging 과 logging의 handler를 import
	
	- __init__.py 를 쓰지않으면 이렇게 하위 모듈 (= logging.handler) 를 별도로 가져와야 하는 경우도 있다.
	
	 
	
	2) logging.Formatter
	
	- 어떤 형식으로 로그가 생성될지를 정한다
	
	→ 여기서는 로그 생성시간(ms 단위까지) + "," + 메시지로 carLogFormatter 설정
	
	- %(asctimes)s 는 로그가 기록되는 시간
	
	- %(message)s 는 입력한 로그가 된다.
	
	 
	
	3) handler.TimedRotatingFileHandler
	
	- 링크 참조: https://docs.python.org/3/library/logging.handlers.html#timedrotatingfilehandler
	
	- 새로운 파일을 만드는 기준
	
	- 저장할 파일명은 car.log
	
	- when='midnight'의 경우 매일밤 자정에 새로운 파일이 만들어진다.
	
	- 이때 만들어지는 형식은 suffix에 따라 설정된다.
	
	→ 예를 들면 여기서는 carLogHandler.suffix = "%Y%m%d" 이므로 car.log.20180504
	
	-
	
	4) 실제 사용할 logger를 생성하고 설정
	
	- carLogger 를 만들고
	
	- 출력레벨을 INFO 이상으로 설정하고
	
	- handler를 추가
	
	 
	
	5) 실제 사용
	
	- carLogger.info("car is coming") 라고 사용하면
	
	- 2018-05-04 08:52:11, 599,car is coming 이라고 car.log 라는 파일에 저장이 된다.
	
	→ 밤 12시가 지나면 car.log.20180504 와 같은 이름으로 다른 파일이 생성됨
```

```
파이썬 self 이해하기

self는 객체의 인스턴스 그 자체를 말한다. 
즉, 객체 자기 자신을 참조하는 매개변수
객체지향 언어는 모두 이걸 메소드에 안보이게 전달하지만, 파이썬은 클래스의 메소드를 정의할 때 self를 명시한다.
메소드를 불러올 때 self는 자동으로 전달된다. self를 사용함으로 클래스내에 정의한 멤버에 접근할 수 있게된다.

근데 그래서 tacotron.py 에서 왜 self를 쓰는지 이해가 안 됨..
```



### 2021-03-15

```
STT, TTS는 안드로이드에서 바로 구현하기
```



### 2021-03-16

```
1. VR에서 멀티버스 구현하기

PUN(Photon Unity Networking) : 멀티플레이어 게임용 유니티 패키지 사용
```

```
2. 모션 인식

tensorflow.js / https://github.com/iconms12/Image_Captioning (pythorch 이미지 캡셔닝)
YOLO / 모션 인식 API 등 자료 조사 필요
```



### 2021-03-17

ec2에 nginx 설치하고 html 배포하기

```
$ sudo apt-get update
$ sudo apt-get install nginx
```

sites-available로 가서 default 파일을 수정한다.

```
$ cd /etc/nginx/sites-available
```

default

root /home/ubuntu/s04p22a401/Web/eriene; (index.html 이 있는 위치) 로 수정 후 nginx 시작

```
$ systemctl start nginx
```

주소로 들어가서 잘 나오는지 확인

```
http://j4a401.p.ssafy.io/
```



### 2021-03-18

```
photon unity network 사용준비

- 유니티 2019.04 (LTS 버전 다운) -> Unity Hub: 유니티 버전 관리를 쉽게 해주는 툴
  (모듈 추가 Android Build Support, iOS Build Support, WebGL Build Support, 		Windows Build Support, 한국어)
- unity asset store에서 photon 추가
```



### 2021-03-19

```
unity에 photon import하기

- Unity asset store에서 PUN 다운한 뒤 appId 발급받기
- Unity 실행 -> Window -> asset store -> PUN import -> appId 붙여넣기
```

```
unity VScode에서 작업하기 (VS말고)
유니티 연동에 필요한 의존 라이브러리 설치
- 깃: https://git-scm.com
- 닷넷 코어: https://microsoft.com/net/core
- 모노: http://www.mono-project.com/download/
```



![keystore 생성](C:\Users\multicampus\AppData\Roaming\Typora\typora-user-images\image-20210319142628495.png)



### 2021-03-22

```
Unity-Firebase 연동

firebase에서 프로젝트(Unity, Android) google-services.json을 발급받은 뒤 
Unity 프로젝트 -> asset 폴더 내에 갖다 놓기

Streaming assets/firebase-services-desktop.json이 생성되면 인식 완료
!! 하지만 unable to load google-services-desktop.json 등 파베가 로드 안 되는 문제가 발생했을 때
```

```
* unable to load google-services-desktop.json 해결하기

1. 현재 해결방법은 없이 unity 2019.3.15f버전으로 다운그레이드 하였다....?!
	-> 우리는 2019.4인데,,,, ㅜ 일단 흐린눈,,
	
2. google-services.json 파일 때문이었는데, 파일 위치를 StreamingAssets로 옮겨주면 해결된다.
	-> 해결 안 된다.^^
	
3. https://firebase.google.com/docs/unity/setup?hl=ko 역시 공식문서 참조하기 ㅎ..
    .NET 4.x를 사용하는 경우 다음과 같은 방법으로 컴파일 오류를 해결하세요.

    모든 플랫폼에서 다음 DLL을 삭제하거나 사용 중지합니다.
    Parse/Plugins/Unity.Compat.dll
    Parse/Plugins/Unity.Tasks.dll
    모든 플랫폼에서 다음 DLL을 사용 설정합니다.
    Parse/Plugins/dotNet45/Unity.Compat.dll
    Parse/Plugins/dotNet45/Unity.Tasks.dll
    
    ....
    
4. 경로에 한글을 다 없앰 --> 정답...!! (경로에 한글은 앵간함 넣지 말자...)
```



### 2021-03-23

```
Android-Unity 연동위해 Android Studio plugin 작업 필요 

- 참조
https://xinyustudio.wordpress.com/2015/12/31/step-by-step-guide-for-developing-android-plugin-for-unity3d-i/

```

프론트 배포하는 방법 정리

- EC2에 HTML 배포하기
  https://www.notion.so/EC2-HTML-ee65722e4ed7484e88cc55b7cc6517f6

1. EC2 접속(mobaXtreme 가능)

   ```
   $ ssh -i J4A401T.pem ubuntu@j4a401.p.ssafy.io
   ```

2. ec2에 nginx 설치하고 html 배포하기

   ```
   $ sudo apt-get update
   $ sudo apt-get install nginx
   ```

3. git clone https://lab.ssafy.com/s04-ai-speech-sub3/s04p23a401.git 하고 index.html 위치 확인

4. sites-available로 가서 default 파일을 수정한다.

   ![https://user-images.githubusercontent.com/43662673/112101474-0a849000-8bea-11eb-8e5c-dba07af2414b.png](https://user-images.githubusercontent.com/43662673/112101474-0a849000-8bea-11eb-8e5c-dba07af2414b.png)

   ```
   $ cd ~
   $ cd /etc/nginx/sites-available
   $ sudo vi default
   ```

   4 - 1. default 파일 수정

   ![https://user-images.githubusercontent.com/43662673/112101684-6b13cd00-8bea-11eb-8b13-b0c3ba33ad7a.png](https://user-images.githubusercontent.com/43662673/112101684-6b13cd00-8bea-11eb-8b13-b0c3ba33ad7a.png)

   root /home/ubuntu/s04p22a401/Web/eriene; (index.html 이 있는 위치) 로 수정 후 nginx 시작

   ```
   $ systemctl start nginx
   ```

5. 주소로 들어가서 잘 나오는지 확인

   ```
   <http://j4a401.p.ssafy.io/>
   ```



- EC2에 HTML 업데이트하기

  https://www.notion.so/EC2-HTML-b8e0513e699c402d96a0c3c99023d8c6

  1. EC2 접속(mobaXtreme 가능)

     ```
     $ ssh -i J4A401T.pem ubuntu@j4a401.p.ssafy.io
     ```

  2. git directory로 이동

  ![https://user-images.githubusercontent.com/43662673/112101929-d3fb4500-8bea-11eb-8c21-eac62ae23c7e.png](https://user-images.githubusercontent.com/43662673/112101929-d3fb4500-8bea-11eb-8c21-eac62ae23c7e.png)

  ```
  $ cd s04p23a401
  $ git pull
  $ sudo service nginx restart
  ```

  3. 주소로 들어가서 잘 나오는지 확인

  ```
  http://j4a401.p.ssafy.io/
  ```
