# ๊ฐ๋ฐ ์ผ์ง ๐ฑโ๐

> ์ฒญํ ๊ฐ๋ฐ ์ผ์ง 

<br>

### 2021-03-10

- ์๊น๋ณ ๋งต ์ปจ์ ์ ํ๊ธฐ

  | ์๊น        | ์๋ฏธ                                                         |
  | ----------- | ------------------------------------------------------------ |
  | ๋นจ๊ฐ        | ๋ธ์ ์ง๋ ์ปจ์ (์ผ์ ๋ง์น๊ณ  ์ง์ ๋์์ค๋ ๊ธธ ๋ธ์์ด ์ง๊ณ  ์๋ ๋๋) |
  | ์ฃผํฉ        | ๋จํ์ผ๋ก ๋ฌผ๋ค์ด ์๋ ๊ธธ์ ๊ฑท๋ (๊ฐ์์ ๋ง์ ํ๋์ ๋ณด์ฌ์ฃผ๊ธฐ โ ๊ฒฝ์พ ๋์ฒ) |
  | ๋ธ๋        | ํฉ๊ธ๋น ๊ฑด๋ฌผ์ด๋ ์ฌ๋ง (์ฌ๋ง์ ์ฝ๊ฐ ํฉํํ ๋๋์ด ์์ ์๋ ์์ผ๋๊น ํฉ๊ธ๋น ๊ฑด๋ฌผ ์์ ํํํ๋ ๋๋...) |
  | ์ด๋ก        | ์ค์๊ธธ ๊ฑธ์ผ๋ฉด์ ์๋ฌผ๋ค๊ณผ ์ํตํ๋ ๋๋ (ํผํค์น๋~)           |
  | ํ๋        | ๋ฐ๋ค, ์ฌ์์ ๊ธธ ๋ฐ๋ผ๊ฐ๋ฉด์ ~~ (์กฐ์ฝ๋, ๋ถ๊ฐ์ฌ๋ฆฌ ๊ฐ์ ๊ฑฐ๋ ์ํธ์์ฉ) ์๋๋ฉด ๋ฐฐ ํ๊ณ  ๋ค๋๋ฉด์ |
  | ์ง์ฒญ        | ๋ณด๋ฆ๋ฌ ๋ฌ ๋ฐค, ํํ๋ก์ด ๋๋                                  |
  | ๋ณด๋ผ        | ๋ณด๋๋น ์ฒ ์ ํํ  (๋ชฝํ์ ์ธ ๋๋)                           |
  | ์์ฃผ (ํํฌ) |                                                              |

  

- ํ์์ค

๋นจ๊ฐ - ํฌ๋ฆฌ์ค๋ง์ค ๋ฐฉ, ๋๋ก 

๋ธ๋ - ํฉ๊ธ๋น ๊ฑด๋ฌผ

ํ๋ - ๋ํ์  ๋ณด๋ฌผ์์, ์ด์  

์ง์ฒญ - ๋ฐฐํ๊ณ  ๋ฐ๋ง๋ถ์ด



### 2021-03-11

SubPJT1 ํ๋ฉด์ ์๊ธด ์๋ฌ

1.  raise RuntimeError(message)

ํด๊ฒฐ ๋ฐฉ๋ฒ:

```
File "/home/gerald/miniconda3/envs/maskrcnn_benchmark/lib/python3.8/site-packages/torch/utils/cpp_extension.py", line 1413, in _run_ninja_build
raise RuntimeError(message)
RuntimeError: Error compiling objects for extension

์ด ์๋ฌ๊ฐ ๋ด์ ๋: ํ์ฌ ์ค์น๋์ด์๋ CUDA์ ๋ง์ง์์ pytorch ํจํค์ง๊ฐ ์ค์น๋์ด ์์ด์ ์๊ธด ๋ฌธ์ 

1) ํ์ฌ ์ค์น๋์ด์๋ cuda ๋ฒ์ ๊ณผ ๋ง๋ pytorch ํจํค์ง๋ฅผ ์ค์น
conda install pytorch torchvision cudatoolkit=11.2 -c pytorch

conda install pytorch torchvision cudatoolkit=10.0 -c pytorch

2) ๋ง์ฝ image_captioning.py๋ฅผ ์คํํ  ๋ DLL load failed๊ฐ ๋ฌ๋ค๋ฉด
ํ๊ฒฝ ๋ณ์์ 'C:\ProgramData\Anaconda3\Library\bin' ๋ฅผ ์ถ๊ฐํด์ค๋ค

๋ง์ฝ ๊ทธ๋๋ ์ ๋๋ฉด Intel-openmp์ ์ค์นํด๋ณธ๋ค.. ์ฐธ๊ณ : https://mclearninglab.tistory.com/30
```

2. DLL load failed : ์ง์ ๋ ๋ชจ๋์ด ~ 

ํด๊ฒฐ๋ฐฉ๋ฒ:

```
CuDNN ๋ฒ์ , pytorch ๋ฒ์ , cuda ๋ฒ์ ์ ๋ง์ถฐ์ผ ํจ
```



### 2021-03-12

```
logging ์ฌ์ฉํ๊ธฐ

์ฌ์ฉํ๋ ์ด์ : 
	- ํ์ด์ฌ ํ๋ก๊ทธ๋จ์์ ๋ฐ์ํ ๋ก๊ทธ๋ฅผ ํ์ผ๋ก ๊ธฐ๋กํ๋ค.
	- ๋งค์ผ ์๋ก์ด ํ์ผ์ด ์์ฑ๋๋ฉฐ, ์์ฑ๋ ์ง๋ฅผ ํ์ผ๋ช์ ๋ฃ๊ณ  ์ถ๋ค.

์ฌ์ฉ ๋ฐฉ๋ฒ: 
	1) logging ๊ณผ logging์ handler๋ฅผ import
	
	- __init__.py ๋ฅผ ์ฐ์ง์์ผ๋ฉด ์ด๋ ๊ฒ ํ์ ๋ชจ๋ (= logging.handler) ๋ฅผ ๋ณ๋๋ก ๊ฐ์ ธ์์ผ ํ๋ ๊ฒฝ์ฐ๋ ์๋ค.
	
	 
	
	2) logging.Formatter
	
	- ์ด๋ค ํ์์ผ๋ก ๋ก๊ทธ๊ฐ ์์ฑ๋ ์ง๋ฅผ ์ ํ๋ค
	
	โ ์ฌ๊ธฐ์๋ ๋ก๊ทธ ์์ฑ์๊ฐ(ms ๋จ์๊น์ง) + "," + ๋ฉ์์ง๋ก carLogFormatter ์ค์ 
	
	- %(asctimes)s ๋ ๋ก๊ทธ๊ฐ ๊ธฐ๋ก๋๋ ์๊ฐ
	
	- %(message)s ๋ ์๋ ฅํ ๋ก๊ทธ๊ฐ ๋๋ค.
	
	 
	
	3) handler.TimedRotatingFileHandler
	
	- ๋งํฌ ์ฐธ์กฐ: https://docs.python.org/3/library/logging.handlers.html#timedrotatingfilehandler
	
	- ์๋ก์ด ํ์ผ์ ๋ง๋๋ ๊ธฐ์ค
	
	- ์ ์ฅํ  ํ์ผ๋ช์ car.log
	
	- when='midnight'์ ๊ฒฝ์ฐ ๋งค์ผ๋ฐค ์์ ์ ์๋ก์ด ํ์ผ์ด ๋ง๋ค์ด์ง๋ค.
	
	- ์ด๋ ๋ง๋ค์ด์ง๋ ํ์์ suffix์ ๋ฐ๋ผ ์ค์ ๋๋ค.
	
	โ ์๋ฅผ ๋ค๋ฉด ์ฌ๊ธฐ์๋ carLogHandler.suffix = "%Y%m%d" ์ด๋ฏ๋ก car.log.20180504
	
	-
	
	4) ์ค์  ์ฌ์ฉํ  logger๋ฅผ ์์ฑํ๊ณ  ์ค์ 
	
	- carLogger ๋ฅผ ๋ง๋ค๊ณ 
	
	- ์ถ๋ ฅ๋ ๋ฒจ์ INFO ์ด์์ผ๋ก ์ค์ ํ๊ณ 
	
	- handler๋ฅผ ์ถ๊ฐ
	
	 
	
	5) ์ค์  ์ฌ์ฉ
	
	- carLogger.info("car is coming") ๋ผ๊ณ  ์ฌ์ฉํ๋ฉด
	
	- 2018-05-04 08:52:11, 599,car is coming ์ด๋ผ๊ณ  car.log ๋ผ๋ ํ์ผ์ ์ ์ฅ์ด ๋๋ค.
	
	โ ๋ฐค 12์๊ฐ ์ง๋๋ฉด car.log.20180504 ์ ๊ฐ์ ์ด๋ฆ์ผ๋ก ๋ค๋ฅธ ํ์ผ์ด ์์ฑ๋จ
```

```
ํ์ด์ฌ self ์ดํดํ๊ธฐ

self๋ ๊ฐ์ฒด์ ์ธ์คํด์ค ๊ทธ ์์ฒด๋ฅผ ๋งํ๋ค. 
์ฆ, ๊ฐ์ฒด ์๊ธฐ ์์ ์ ์ฐธ์กฐํ๋ ๋งค๊ฐ๋ณ์
๊ฐ์ฒด์งํฅ ์ธ์ด๋ ๋ชจ๋ ์ด๊ฑธ ๋ฉ์๋์ ์๋ณด์ด๊ฒ ์ ๋ฌํ์ง๋ง, ํ์ด์ฌ์ ํด๋์ค์ ๋ฉ์๋๋ฅผ ์ ์ํ  ๋ self๋ฅผ ๋ช์ํ๋ค.
๋ฉ์๋๋ฅผ ๋ถ๋ฌ์ฌ ๋ self๋ ์๋์ผ๋ก ์ ๋ฌ๋๋ค. self๋ฅผ ์ฌ์ฉํจ์ผ๋ก ํด๋์ค๋ด์ ์ ์ํ ๋ฉค๋ฒ์ ์ ๊ทผํ  ์ ์๊ฒ๋๋ค.

๊ทผ๋ฐ ๊ทธ๋์ tacotron.py ์์ ์ self๋ฅผ ์ฐ๋์ง ์ดํด๊ฐ ์ ๋จ..
```



### 2021-03-15

```
STT, TTS๋ ์๋๋ก์ด๋์์ ๋ฐ๋ก ๊ตฌํํ๊ธฐ
```



### 2021-03-16

```
1. VR์์ ๋ฉํฐ๋ฒ์ค ๊ตฌํํ๊ธฐ

PUN(Photon Unity Networking) : ๋ฉํฐํ๋ ์ด์ด ๊ฒ์์ฉ ์ ๋ํฐ ํจํค์ง ์ฌ์ฉ
```

```
2. ๋ชจ์ ์ธ์

tensorflow.js / https://github.com/iconms12/Image_Captioning (pythorch ์ด๋ฏธ์ง ์บก์๋)
YOLO / ๋ชจ์ ์ธ์ API ๋ฑ ์๋ฃ ์กฐ์ฌ ํ์
```



### 2021-03-17

ec2์ nginx ์ค์นํ๊ณ  html ๋ฐฐํฌํ๊ธฐ

```
$ sudo apt-get update
$ sudo apt-get install nginx
```

sites-available๋ก ๊ฐ์ default ํ์ผ์ ์์ ํ๋ค.

```
$ cd /etc/nginx/sites-available
```

default

root /home/ubuntu/s04p22a401/Web/eriene; (index.html ์ด ์๋ ์์น) ๋ก ์์  ํ nginx ์์

```
$ systemctl start nginx
```

์ฃผ์๋ก ๋ค์ด๊ฐ์ ์ ๋์ค๋์ง ํ์ธ

```
http://j4a401.p.ssafy.io/
```



### 2021-03-18

```
photon unity network ์ฌ์ฉ์ค๋น

- ์ ๋ํฐ 2019.04 (LTS ๋ฒ์  ๋ค์ด) -> Unity Hub: ์ ๋ํฐ ๋ฒ์  ๊ด๋ฆฌ๋ฅผ ์ฝ๊ฒ ํด์ฃผ๋ ํด
  (๋ชจ๋ ์ถ๊ฐ Android Build Support, iOS Build Support, WebGL Build Support, 		Windows Build Support, ํ๊ตญ์ด)
- unity asset store์์ photon ์ถ๊ฐ
```



### 2021-03-19

```
unity์ photon importํ๊ธฐ

- Unity asset store์์ PUN ๋ค์ดํ ๋ค appId ๋ฐ๊ธ๋ฐ๊ธฐ
- Unity ์คํ -> Window -> asset store -> PUN import -> appId ๋ถ์ฌ๋ฃ๊ธฐ
```

```
unity VScode์์ ์์ํ๊ธฐ (VS๋ง๊ณ )
์ ๋ํฐ ์ฐ๋์ ํ์ํ ์์กด ๋ผ์ด๋ธ๋ฌ๋ฆฌ ์ค์น
- ๊น: https://git-scm.com
- ๋ท๋ท ์ฝ์ด: https://microsoft.com/net/core
- ๋ชจ๋ธ: http://www.mono-project.com/download/
```



![keystore ์์ฑ](C:\Users\multicampus\AppData\Roaming\Typora\typora-user-images\image-20210319142628495.png)



### 2021-03-22

```
Unity-Firebase ์ฐ๋

firebase์์ ํ๋ก์ ํธ(Unity, Android) google-services.json์ ๋ฐ๊ธ๋ฐ์ ๋ค 
Unity ํ๋ก์ ํธ -> asset ํด๋ ๋ด์ ๊ฐ๋ค ๋๊ธฐ

Streaming assets/firebase-services-desktop.json์ด ์์ฑ๋๋ฉด ์ธ์ ์๋ฃ
!! ํ์ง๋ง unable to load google-services-desktop.json ๋ฑ ํ๋ฒ ๊ฐ ๋ก๋ ์ ๋๋ ๋ฌธ์ ๊ฐ ๋ฐ์ํ์ ๋
```

```
* unable to load google-services-desktop.json ํด๊ฒฐํ๊ธฐ

1. ํ์ฌ ํด๊ฒฐ๋ฐฉ๋ฒ์ ์์ด unity 2019.3.15f๋ฒ์ ์ผ๋ก ๋ค์ด๊ทธ๋ ์ด๋ ํ์๋ค....?!
	-> ์ฐ๋ฆฌ๋ 2019.4์ธ๋ฐ,,,, ใ ์ผ๋จ ํ๋ฆฐ๋,,
	
2. google-services.json ํ์ผ ๋๋ฌธ์ด์๋๋ฐ, ํ์ผ ์์น๋ฅผ StreamingAssets๋ก ์ฎ๊ฒจ์ฃผ๋ฉด ํด๊ฒฐ๋๋ค.
	-> ํด๊ฒฐ ์ ๋๋ค.^^
	
3. https://firebase.google.com/docs/unity/setup?hl=ko ์ญ์ ๊ณต์๋ฌธ์ ์ฐธ์กฐํ๊ธฐ ใ..
    .NET 4.x๋ฅผ ์ฌ์ฉํ๋ ๊ฒฝ์ฐ ๋ค์๊ณผ ๊ฐ์ ๋ฐฉ๋ฒ์ผ๋ก ์ปดํ์ผ ์ค๋ฅ๋ฅผ ํด๊ฒฐํ์ธ์.

    ๋ชจ๋  ํ๋ซํผ์์ ๋ค์ DLL์ ์ญ์ ํ๊ฑฐ๋ ์ฌ์ฉ ์ค์งํฉ๋๋ค.
    Parse/Plugins/Unity.Compat.dll
    Parse/Plugins/Unity.Tasks.dll
    ๋ชจ๋  ํ๋ซํผ์์ ๋ค์ DLL์ ์ฌ์ฉ ์ค์ ํฉ๋๋ค.
    Parse/Plugins/dotNet45/Unity.Compat.dll
    Parse/Plugins/dotNet45/Unity.Tasks.dll
    
    ....
    
4. ๊ฒฝ๋ก์ ํ๊ธ์ ๋ค ์์ฐ --> ์ ๋ต...!! (๊ฒฝ๋ก์ ํ๊ธ์ ์ต๊ฐํจ ๋ฃ์ง ๋ง์...)
```



### 2021-03-23

```
Android-Unity ์ฐ๋์ํด Android Studio plugin ์์ ํ์ 

- ์ฐธ์กฐ
https://xinyustudio.wordpress.com/2015/12/31/step-by-step-guide-for-developing-android-plugin-for-unity3d-i/

```

ํ๋ก ํธ ๋ฐฐํฌํ๋ ๋ฐฉ๋ฒ ์ ๋ฆฌ

- EC2์ HTML ๋ฐฐํฌํ๊ธฐ
  https://www.notion.so/EC2-HTML-ee65722e4ed7484e88cc55b7cc6517f6

1. EC2 ์ ์(mobaXtreme ๊ฐ๋ฅ)

   ```
   $ ssh -i J4A401T.pem ubuntu@j4a401.p.ssafy.io
   ```

2. ec2์ nginx ์ค์นํ๊ณ  html ๋ฐฐํฌํ๊ธฐ

   ```
   $ sudo apt-get update
   $ sudo apt-get install nginx
   ```

3. git clone https://lab.ssafy.com/s04-ai-speech-sub3/s04p23a401.git ํ๊ณ  index.html ์์น ํ์ธ

4. sites-available๋ก ๊ฐ์ default ํ์ผ์ ์์ ํ๋ค.

   ![https://user-images.githubusercontent.com/43662673/112101474-0a849000-8bea-11eb-8e5c-dba07af2414b.png](https://user-images.githubusercontent.com/43662673/112101474-0a849000-8bea-11eb-8e5c-dba07af2414b.png)

   ```
   $ cd ~
   $ cd /etc/nginx/sites-available
   $ sudo vi default
   ```

   4 - 1. default ํ์ผ ์์ 

   ![https://user-images.githubusercontent.com/43662673/112101684-6b13cd00-8bea-11eb-8b13-b0c3ba33ad7a.png](https://user-images.githubusercontent.com/43662673/112101684-6b13cd00-8bea-11eb-8b13-b0c3ba33ad7a.png)

   root /home/ubuntu/s04p22a401/Web/eriene; (index.html ์ด ์๋ ์์น) ๋ก ์์  ํ nginx ์์

   ```
   $ systemctl start nginx
   ```

5. ์ฃผ์๋ก ๋ค์ด๊ฐ์ ์ ๋์ค๋์ง ํ์ธ

   ```
   <http://j4a401.p.ssafy.io/>
   ```



- EC2์ HTML ์๋ฐ์ดํธํ๊ธฐ

  https://www.notion.so/EC2-HTML-b8e0513e699c402d96a0c3c99023d8c6

  1. EC2 ์ ์(mobaXtreme ๊ฐ๋ฅ)

     ```
     $ ssh -i J4A401T.pem ubuntu@j4a401.p.ssafy.io
     ```

  2. git directory๋ก ์ด๋

  ![https://user-images.githubusercontent.com/43662673/112101929-d3fb4500-8bea-11eb-8c21-eac62ae23c7e.png](https://user-images.githubusercontent.com/43662673/112101929-d3fb4500-8bea-11eb-8c21-eac62ae23c7e.png)

  ```
  $ cd s04p23a401
  $ git pull
  $ sudo service nginx restart
  ```

  3. ์ฃผ์๋ก ๋ค์ด๊ฐ์ ์ ๋์ค๋์ง ํ์ธ

  ```
  http://j4a401.p.ssafy.io/
  ```
