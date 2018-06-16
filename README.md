
## Simple Docker Node App

based on these instructions:
https://nodejs.org/en/docs/guides/nodejs-docker-webapp/

```
docker build -t ultrasaurus/node-web-app .
docker run -p 49160:8080 -d ultrasaurus/node-web-app
curl -i localhost:49160
```



output:
```
> docker_web_app@1.0.0 start /usr/src/app
> node server.js

Running on http://0.0.0.0:8080
airtime:awsnode sallen$ curl -i localhost:49160
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: text/html; charset=utf-8
Content-Length: 12
ETag: W/"c-M6tWOb/Y57lesdjQuHeB1P/qTV0"
Date: Sat, 16 Jun 2018 15:28:03 GMT
Connection: keep-alive

Hello world
```