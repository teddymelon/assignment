## 如何通過DOCKERFILE，調整Nginx內的預設頁面
### 主要思路
- [x] 如何將sre.txt放進容器內
    -  直接通過docker指令連線進容器內新增與修改 ``` docker exec -it name /bin/sh ```
    -  通過Dockerfile編寫，把需要的內容放進nginx的預設路徑下

### Dockerfile撰寫
由於要追求自動化，因此當然不可能建好Docker才將sre.txt放進容器內，因此直接透過第二種方式來進行，也就是**通過Dockerfile的編寫**，把需要的內容放進nginx的預設網頁路徑下。

```
FROM nginx:latest
# 取得最新的Nginx鏡像

MAINTAINER TeddyMelon
#作者是我啦！

RUN echo 'Hello SRE!' > /usr/share/nginx/html/sre.txt
#把sre.txt放到Nginx網頁路徑底下

EXPOSE 80
#宣告哪個Port，預設就用80吧！

CMD [ "nginx", "-g", "daemon off;" ]
#Docker運行時，執行的命令，確保nginx可以正常啟動
```


### Docker Image打包
**記得切換到DockerFile所在的路徑底下**

1.``` docker build -t topic-2:v1 . ```

2.``` docker images ```


```
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
topic-2      v1        67747540e76b   23 minutes ago   187MB
nginx        latest    a6bd71f48f68   2 weeks ago      187MB 
```

### 打包後的動作
接下來就可以看是要上傳到哪個Repository上，這次會先放在dockerhub以及AWS的ECR中(ECR也可以決定放在私有庫或者公開庫上，本次實作都有放上)

**Dockerhub**

1.``` docker login ```

2.``` docker tag 677475 teddymelon/topic-2:latest ```

3.``` docker push teddymelon/topic-2:latest ```

**AWS ECR Public**

1.``` aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/xxxxxxxx ```

2.``` docker tag 677475 public.ecr.aws/xxxxxxxx/teddy:latest ```

3.``` docker push public.ecr.aws/xxxxxxxx/teddy:latest ```

**AWS ECR Private**

1.``` aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin xxxxxxxxxxxx.dkr.ecr.us-east-1.amazonaws.com ```

2.``` docker tag assignment:latest xxxxxxxxxxxx.dkr.ecr.us-east-1.amazonaws.com/assignment:latest ```

3.``` docker push xxxxxxxxxxxx.dkr.ecr.us-east-1.amazonaws.com/assignment:latest ```