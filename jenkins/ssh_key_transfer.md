# 빌드서버와 스테이지 서버간의 키를 교환하자.
## [전체 젠킨스 문서](index.md)
## 1. 빌드 서버 키 생성
### 1.1. 사용자를 jenkins로 변경
```
sudo su jenkins
cd
```
### 1.2. 키 생성
```
ssh-keygen -t rsa -m pem
엔터 3회
```
### 1.3. 공개키 복사
```
cat .ssh/id_rsa.pub
```

## 2. 스테이지 서버에 키 등록
### 2.1. 사용자를 tomcat으로 변경
```
sudo su tomcat
cd
```
### 2.2. 빌드 서버의 공개키를 스테이지 서버에 복사
```
vi .ssh/authorized_keys
#1.3 복사
```
> 개행 주의

## [맨 위로](#)