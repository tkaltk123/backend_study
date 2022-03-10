# 도커에 젠킨스를 설치하자.
## [전체 젠킨스 문서](index.md)
> 사전에 docker가 설치되어야 한다. [참조]
## 1. 도커 컨테이너 생성
### 1.1. DockerFile 생성
> 컨테이너가 저장될 볼륨에 DockerFile을 생성해준다.
```dockerfile
#DockerFile
FROM jenkins/jenkins:lts 
USER root 
RUN apt-get update && \
    apt-get -y install apt-transport-https \ 
        ca-certificates \ 
        curl \ 
        gnupg2 \ 
        zip \ 
        unzip \ 
        software-properties-common && \ 
    curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \ 
    add-apt-repository \ 
    "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \ 
    $(lsb_release -cs) \ 
    stable" && \ 
    apt-get update && \ 
    apt-get -y install docker-ce

```
### 1.2. docker-compose.yml 생성
> 1.1.과 같은 폴더에 docker-compose.yml을 생성해준다.
```yml
# docker-compose.yml 
version: '3.7'
services: 
  jenkins: 
    build: 
      context: . 
    container_name: jenkins 
    user: root 
    ports: 
      - 9000:8080 
      - 50000:50000
    volumes: 
      - ./jenkins_home:/var/jenkins_home 
      - //var/run/docker.sock:/var/run/docker.sock
```
> 브라우저를 통해 접속할 포트를 8080 포트와 연결  
> 이 문서에서는 9000번과 연결함  
> 로컬인 경우 localhost:9000으로 jenkins 로그인
### 1.3. 컨테이너 생성
> docker-compose.yml과 DockerFile이 함께 저장된 위치에서 다음 명령 실행
```
docker-compose up -d
```
### 1.4. 초기 비밀번호 위치
```
 jenkins_home/secrets/initialAdminPassword
```
### 1.5. 생성된 키페어 위치
```
/var/jenkins_home/.ssh/id_rsa
```
## [맨 위로](#)