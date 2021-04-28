EC2에 HTML 배포하기



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

   ![image](https://user-images.githubusercontent.com/43662673/112101474-0a849000-8bea-11eb-8e5c-dba07af2414b.png)

   ```
   $ cd ~
   $ cd /etc/nginx/sites-available
   $ sudo vi default
   ```

   4 - 1. default 파일 수정

   ![image](https://user-images.githubusercontent.com/43662673/112101684-6b13cd00-8bea-11eb-8b13-b0c3ba33ad7a.png)

   root /home/ubuntu/s04p22a401/Web/eriene; (index.html 이 있는 위치) 로 수정 후 nginx 시작

   ```
   $ systemctl start nginx
   ```

5. 주소로 들어가서 잘 나오는지 확인

   ```
   http://j4a401.p.ssafy.io/
   ```