여러 에러들



```
Could not open lock file /var/lib/apt/lists/lock - open (13: Permission denied)

1. sudo su, su 로 관리자 계정으로 넘어간다
2. $ rm /var/lib/apt/lists/lock
3. $ rm /var/cached/apt/archives/lock

그 다음 $ apt-get upgrade -y 하면 apt-get이 에러 없이 잘 되는 것을 볼 수 있다.
```

2. E: The repository 'http://ppa.launchpad.net/certbot/certbot/ubuntu focal Release' does not have a Release file. 에러

![image-20210323195500613](C:\Users\0901B\AppData\Roaming\Typora\typora-user-images\image-20210323195500613.png)

```
sudo apt-add-repository -r ppa:certbot/certbot
```

After that, the following commands do not generate any errors:

```
sudo apt update
sudo apt-get update
```

