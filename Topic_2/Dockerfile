FROM nginx:latest
# 取得最新的Nginx鏡像
MAINTAINER TeddyMelon
RUN echo 'Hello SRE!' > /usr/share/nginx/html/sre.txt
#把sre.txt放到Nginx網頁路徑底下
EXPOSE 80
CMD [ "nginx", "-g", "daemon off;" ]
#Docker運行時，執行的命令，確保nginx可以正常啟動