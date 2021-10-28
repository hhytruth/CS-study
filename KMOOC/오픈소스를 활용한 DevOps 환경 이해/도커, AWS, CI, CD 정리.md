

```
#docker 명령어 실행시 sudo를 매번 치는게 귀찮을 때 하는 설정

# 현재 유저 확인
echo $USER

# 현재 유저 출력결과
ubuntu

# docker 그룹에 현재 유저 추가
sudo usermod -aG docker $USER

# docker 재실행
sudo service docker restart

# 그래도 적용이 안된경우 접속해제 후 재연결
exit
```





0 - AWS EC2는 생성되어 받아온 상태이기 때문에 생략.. EC2 서버로의 접속은 Xshell을 이용하여 접속하였다.



https://insight.infograb.net/docs/aws/installing-docker-on-aws-ec2/

1 - 인스턴스 안에 Docker 설치

sudo apt-get update

sudo apt-get install



### 자동 설치 스크립트로 도커 설치하기

도커는 리눅스 배포판 종류를 자동으로 인식해 Docker 패키지를 설치해주는 스크립트를 제공한다.



```
sudo wget -qO- https://get.docker.com/ | sh
```



- `wget` : 인터넷에서 파일을 받을 때 사용하는 리눅스 명령어이다.
- `-O` : wget은 다운로드 경로의 마지막 슬래시 다음에 오는 단어를 파일 이름으로 한다. 여기서는 빈칸이 되니 다른 이름으로 저장하는 옵션 -O를 사용한다.
- `-q` : 출력없이 종료한다.
- `| sh` : `|`는 파이프라인, 즉 wget으로 파일을 다운받은 후 셸을 실행한다는 의미이다.



**6. 확인하기**

도커 시스템 확인하기

```
sudo systemctl status docker
```

- `systemctl` : 리눅스에서 서비스를 등록, 삭제(mask, unmask) / 활성화, 비활성화(enable, disable) / 시작, 중지, 재시작(start, stop, restart) / 상태 확인(status) / 서비스 확인(list-units, list-unit-files)을 할 수 있는 명령어



---------

**1. 도커 이미지 파일 생성**

vim 편집기로 도커 파일을 만든다. 도커 파일의 이름은 항상 `Dockerfile` 이어야 한다. 맨 앞의 대문자에 유의한다.



```
sudo vim Dockerfile
```



**2. 도커 파일 작성하기**

운영체제는 우분투 18.04 / nginx 웹서버를 사용하는 도커 파일을 만든다.

아래 코드에 대한 설명은 [가장 빨리 만나는 도커](http://pyrasis.com/book/DockerForTheReallyImpatient/Chapter04/02) 참고!

※ 참고 : EXPOSE 코드와 같은 줄에 주석을 달면 오류가 생긴다



```
FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y nginx # install nginx web server ('yes' or 'yes'~)

VOLUME ["/data", "/etc/nginx/site-enabled", "/var/log/nginx"] 

# Open HTTP port for nginx
EXPOSE 80

WORKDIR /etc/nginx 

CMD ["nginx"] 
```



**3. 빌드**

현재 디렉터리의 이미지파일을 내가 원하는 이름으로 빌드한다. `-t`로 해당 이미지의 repository 이름을 정한다.



```
sudo docker build -t 이미지파일명 .
```



### 컨테이너 띄우기 (이미지 파일 실행)

**1. 서버 포트와 호스트 포트 연결시켜서 run**

`docker run -p 외부포트:내부포트 이미지파일명`. 외부포트 자리가 도커 파일 작성 때 EXPOSE로 명시해줬던 포트 번호이다. 외부 포트를 안써주면 외부포트를 랜덤하게 배치한다.



```
sudo docker run -p 80:80 nginx
```





---------------------

## 1. Jenkins 이미지 내려 받기

Docker Hub 에서 Jenkins 이미지를 내려받을 수 있다.

#### Docker Hub이란?

- 도커 이미지를 업로드해서 공유하는 저장소를 도커 레지스트리(Docker Registry)라고 한다. 대표적으로는 도커의 공식 레지스트리인 Docker Hub 가 있다. 도커 허브에서는 업체에서 제공하는 공식 이미지를 받을 수 있다.
- Ubuntu 나 CentOS 같은 OS 이미지, MySQL, Redis, MongoDB, Nginx 와 같은 미들웨어, OpenJDK, Golang, NodeJS 와 같은 플랫폼 이미지도 제공한다.

### Jenkins 이미지 다운로드

```
sudo docker pull jenkins/jenkins:lts
```



> **2. docker image를 container로 띄우기**

다운로드 받은 jenkins image를 docker container로 띄우도록하자.

```
# docker 컨테이너로 등록 후 실행
docker run -d -p 9090:8080 -v /jenkins:/var/jenkins_home --name jenkins -u root jenkins/jenkins:lts
```

>
>
>[local] /jenkins 경로에 : [jenkins] jenkins_home 연결



접속후 ```호스트아이피:9090``` 으로 접속



> 3. 패스워드 입력

```
# docker의 jenkins 컨테이너로 접속하여 패스워드 파일 확인
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

36cd885828fb4ec2869abd3a05388428

-> 기본 플러그인 설치

-> Create First Admin User 가입



----

### jenkins gitlab 연동



젠킨스에서 Jenkins 관리를 들어가면 플러그인 관리 버튼이 있는데 여기서 GitLab 플러그인을 설치해야한다.



**비밀번호 분실 시**

> Jenkins 설정파일에서 '보안 암호 없음'으로 변경하는 방법
>
> ```
> sudo vi /var/lib/jenkins/config.xml
> 
> ...
> <useSecurity>false</useSecurity>
> ...
> ```
>
> 원래 true로 되어있으나 false로 변경하면 로그인 화면이 나오지않는다.



1. Jenkins 포트 방화벽 오픈 :
   - `sudo iptables -I INPUT 1 -p tcp --dport 9090 -j ACCEPT`
   - `sudo iptables -I OUTPUT 1 -p tcp --dport 9090 -j ACCEPT`



jenkins관리 -> 시스템 설정에서 gitlab 관련 설정 추가.(Credentials는 Gitlab에서 발급받은 API token을 입력하면 된다.)



```shell
pipeline {
    agent any
    tools {nodejs "nodejs"}

    stages {
        stage('test') {
            steps {
                git credentialsId: 'jp2jjj', url: 'https://lab.ssafy.com/s05-bigdata-dist/S05P21C102.git'
            
                dir('service/front') {

                    sh 'npm install'
                    sh 'npm run build'
                }
            } 
        }
        
        stage('Deploy') {
            steps {
                    sh 'dir'
                    sh 'pwd'
                    sh 'scp -i /var/jenkins_home/workspace/c102_front/J5C102T.pem -q -o StrictHostKeyChecking=no -r /var/jenkins_home/workspace/c102_front/service/front/dist ubuntu@j5c102.p.ssafy.io:~'
                    sh "ssh -i /var/jenkins_home/workspace/c102_front/J5C102T.pem ubuntu@j5c102.p.ssafy.io 'pwd'"
                    sh "ssh -i /var/jenkins_home/workspace/c102_front/J5C102T.pem ubuntu@j5c102.p.ssafy.io 'docker cp /home/ubuntu/dist/ web:/var/www/html'"
                    sh "ssh -i /var/jenkins_home/workspace/c102_front/J5C102T.pem ubuntu@j5c102.p.ssafy.io 'docker restart web'"
                
                
            }
        }
    }
}
```







---------

##### Nginx 이미지 pull

```dockerfile
docker pull nginx:latest

docker run --name <설정이름> -d -p 80:80 nginx
```



![image-20210915032023422](C:\Users\jp2jj\AppData\Roaming\Typora\typora-user-images\image-20210915032023422.png)



--------------

mongodb 설정

![image-20210924140916977](C:\Users\jp2jj\AppData\Roaming\Typora\typora-user-images\image-20210924140916977.png)

 docker run --name mongo -p 27017:27017 -v ~/data:/data/db -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=c102 -d mongo



-----------

인증실패

```
docker exec -i -t mongo bash

$mongo

use admin

db.createUser({user: "root", pwd: "c102", roles:["root"]})
```





------------

SCP / SSH



scp -i /var/jenkins_home/workspace/c102_front/J5C102T.pem -q -o StrictHostKeyChecking=no -r





------

리눅스 타임존 설정

sudo rm /etc/localtime

sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime

date





-----------

백엔드 배포

jenkins에서 gradle 플러그인 설치

툴에서 gradle 등록

![image-20210930002915743](C:\Users\jp2jj\AppData\Roaming\Typora\typora-user-images\image-20210930002915743.png)



----------------

그냥 스프링부트 배포

스프링부트 폴더로 이동

chmod 777 gradlew

sudo ./gradlew build

build/libs 폴더로 이동 ```cd build/libs```

nohup java -jar backend-0.0.1-SNAPSHOT.jar &

ps -ef | grep backend-0.0.1-SNAPSHOT.jar 실행시킨 프로세스 확인
