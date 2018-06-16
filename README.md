
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

## AWS with ElasticBeanstalk

```
eb init
```

Note: not all services are available in every region ([AWS doc](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services))

Select a default region:
`1) us-east-1 : US East (N. Virginia)`

Select an application to use:
`2) [ Create new Application ]`

Application Name: `node-web-app`

```
It appears you are using Docker. Is this correct?
(Y/n): Y
```

Select a platform version:  use the lastest, which is the default

Do you wish to continue with CodeCommit? (y/N) (default is n): n

Do you want to set up SSH for your instances?
(Y/n): Y

This creates `.elasticbeanstalk/config.yml` and adds to `.gitignore` so we only have thse files locally


```
eb create node-web-app
```

output:

```
Creating application version archive "app-a1d5-180616_090306".
Uploading node-web-app/app-a1d5-180616_090306.zip to S3. This may take a while.
Upload Complete.
Environment details for: node-web-app
  Application name: node-web-app
  Region: us-east-1
  Deployed Version: app-a1d5-180616_090306
  Environment ID: e-gjhqj9vhgd
  Platform: arn:aws:elasticbeanstalk:us-east-1::platform/Docker running on 64bit Amazon Linux/2.10.0
  Tier: WebServer-Standard-1.0
  CNAME: UNKNOWN
  Updated: 2018-06-16 16:03:11.492000+00:00
Printing Status:
INFO: createEnvironment is starting.
INFO: Using elasticbeanstalk-us-east-1-311722708448 as Amazon S3 storage bucket for environment data.
```

```
eb deploy
```

output:
```
WARNING: You have uncommitted changes.
Creating application version archive "app-a1d5-180616_091448".
Uploading node-web-app/app-a1d5-180616_091448.zip to S3. This may take a while.
Upload Complete.
INFO: Environment update is starting.
INFO: Deploying new version to instance(s).
INFO: Successfully pulled node:8
INFO: Successfully built aws_beanstalk/staging-app
INFO: Docker container 7c9bda3c3674 is running aws_beanstalk/current-app.
INFO: New application version was deployed to running EC2 instances.
INFO: Environment update completed successfully.
```


```
eb open
```

opens a browser window which should display: Hello world

