# 젠킨스 로컬 환경을 구축해보자.
## [전체 젠킨스 문서](index.md)
> 사전에 EC2 인스턴스를 생성해야 한다. [참조](../aws/aws%20ec2.md)
## 1. 스테이지 서버에 톰캣 설치
### 1.1. jdk 설치
- [EC2 젠킨스 설치 - 1.1 참조](jenkins_with_ec2.md#11-jdk-설치)
### 1.2. 톰캣 설치
- 톰캣 다운로드  
    ```
    wget http://archive.apache.org/dist/tomcat/tomcat-8/v8.5.27/bin/apache-tomcat-8.5.27.tar.gz
    ```
- 압축 해제  
    ```
    tar zxvf apache-tomcat-8.5.27.tar.gz
    ```
- /opt/tomcat 디렉토리 생성 후 톰캣 이동
    ```
    sudo mkdir -p /opt/tomcat
    sudo mv apache-tomcat-8.5.27 /opt/tomcat/
    ```
- 톰캣 바로가기 생성
    ```
    sudo ln -s /opt/tomcat/apache-tomcat-8.5.27 /opt/tomcat/latest
    ```
- 톰캣 사용자 생성
    ```
    sudo adduser tomcat
    ```
- 톰캣의 소유자를 tomcat으로 설정
    ```
    sudo chown -R tomcat:tomcat /opt/tomcat
    sudo sh -c 'chmod +x /opt/tomcat/latest/bin/*.sh'
    ```
## [맨 위로](#)