Error response from daemon: conflict: unable to delete ee70e7682367 (must be forced) - image is being used by stopped container 74df76f4a488

![image](https://user-images.githubusercontent.com/43662673/130477109-db0944db-9196-4ced-a425-1677f6c34633.png)

도커의 특정 이미지를 삭제하려 할 때, 멈춰진 컨테이너 때문에 삭제가 되지 않음



```
> docker rm 74df76f4a488
```

먼저 컨테이너를 삭제한 후



```
> docker rmi ee70e7682367 
```

image를 삭제하면 된다.



```
> docker images
```

목록을 보면 삭제된 것을 알 수 있다.

