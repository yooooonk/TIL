# AWS 클라우드 컴퓨팅 설정

## EC2 인스턴스 생성
1. EC2 또는 인스턴스(서버) 설정 - Amazone linux2 ami
2. Elastic IP(탄력적IP) 생성 - 연결
3. pem key 다운로드
4. windows : putty-gen을 이용해 pem key ppk 생성, putty로 ssh 접속

## 서버 설정
- 자바 기반의 웹 애플리케이션(톰캣, 스프링부트)이 작동하려면 필수로 필요한 설정들
1. Java 설치
```sudo yum install -y java-1.8.0-openjdk-devel.x86_64 ```

2. 타임존 변경    
```
sudo rm /etc/localtime   
sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime
```

3. 호스트네임 변경
- 현재 접속한 서버의 별명을 등록. 실무에서는 수십 대의 서버가 작동되는 데, IP만으로 어떤 서버가 어떤 역할을 하는지 알 수가 없으므로 보통 호스트 네임을 필수로 등록한다
```
sudo vim /etc/sysconfig/network
```

## AWS RDS
- AWS에서 지원하는 클라우드 기반 관계형 데이터베이스
- 하드웨어 프로비저닝, 데이터베이스 설정, 패치 및 백업과 같이 잦은 운영 작업을 작동화해 개발자가 개발에 집중할 수 있게 지원하는 서비스

---
__reference__
- &#128214; 스프링부트와 AWS로 혼자 구현하는 웹서비스