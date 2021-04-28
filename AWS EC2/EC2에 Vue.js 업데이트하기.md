1**. EC2 접속**

```jsx
$ ssh -i I4A308T.pem ubuntu@i4a308.p.ssafy.io
```

2. **해당 프로젝트로 이동해서 git pull**

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/56fc11d3-af6e-4d08-9e95-3df6490bad19/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/56fc11d3-af6e-4d08-9e95-3df6490bad19/Untitled.png)

**3.  빌드**

FrontEnd 폴더 들어가서 build하면 frontend/dist에 빌드파일들 자동생성

```jsx
$ npm run build
```

4. 기존 dist 폴더 삭제

```jsx
ubuntu@ip-172-26-1-219:/var/www/html$ sudo rm -r dist
```

**4. dist 폴더 default 폴더로 이동**

```jsx
ubuntu@ip-172-26-1-219:~/s04p13a308/FrontEnd$ sudo mv -f dist/ /var/www/html/
```

**5. nginx 서버 재부팅**

```jsx
ubuntu@ip-172-26-1-219:/etc/nginx/sites-available$ cd /var/www/html
ubuntu@ip-172-26-1-219:/var/www/html$ sudo service nginx restart
```
