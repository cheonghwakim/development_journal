1**. EC2 접속**

```jsx
$ ssh -i I4A308T.pem ubuntu@i4a308.p.ssafy.io
```

**2. nginx 설치**

```jsx
$ sudo apt-get update
$ sudo apt-get install nginx
```

**3.  빌드**

FrontEnd 폴더 들어가서 build하면 frontend/dist에 빌드파일들 자동생성

```jsx
$ npm run build
```

**4. nginx default 설정**

```jsx
//해당경로로 이동후 명령어 작성
ubuntu@ip-172-26-1-219:/etc/nginx/sites-available$ sudo vi default
```

```jsx
server {
        listen 80 default_server;
        listen [::]:80 default_server;

			//nginx default 폴더 설정
        root /var/www/html/dist;

        index index.html;

        server_name _;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

**4. dist 폴더 default 폴더로 이동**

```jsx
ubuntu@ip-172-26-1-219:~/s04p13a308/FrontEnd$ sudo mv dist/ /var/www/html/
```

**5. nginx 서버 재부팅**

```jsx
ubuntu@ip-172-26-1-219:/etc/nginx/sites-available$ cd /var/www/html
ubuntu@ip-172-26-1-219:/var/www/html$ sudo service nginx restart
```

디렉토리 삭제 명령어(안에 파일들까지)

/var/www/html/ 에 있는 dist를 삭제 한 다음, FrontEnd에 있는 dist를 이동시킴

sudo rm -r dist

 

1**. EC2 접속**

```jsx
$ ssh -i I4A308T.pem ubuntu@i4a308.p.ssafy.io
```

**2. nginx 설치**

```jsx
$ sudo apt-get update
$ sudo apt-get install nginx
```

**3.  빌드**

FrontEnd 폴더 들어가서 build하면 frontend/dist에 빌드파일들 자동생성

```jsx
$ npm run build
```

**4. nginx default 설정**

```jsx
//해당경로로 이동후 명령어 작성
ubuntu@ip-172-26-1-219:/etc/nginx/sites-available$ sudo vi default
```

```jsx
server {
        listen 80 default_server;
        listen [::]:80 default_server;

			//nginx default 폴더 설정
        root /var/www/html/dist;

        index index.html;

        server_name _;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

**4. dist 폴더 default 폴더로 이동**

```jsx
ubuntu@ip-172-26-1-219:~/s04p13a308/FrontEnd$ sudo mv dist/ /var/www/html/
```

**5. nginx 서버 재부팅**

```jsx
ubuntu@ip-172-26-1-219:/etc/nginx/sites-available$ cd /var/www/html
ubuntu@ip-172-26-1-219:/var/www/html$ sudo service nginx restart
```

디렉토리 삭제 명령어(안에 파일들까지)

/var/www/html/ 에 있는 dist를 삭제 한 다음, FrontEnd에 있는 dist를 이동시킴

sudo rm -r dist
