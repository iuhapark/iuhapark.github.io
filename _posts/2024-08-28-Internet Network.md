---
title: "Spring Bean, Servlet, 제어 역전 (IoC), 의존성 주입 (DI), AOP (관점 지향 프로그래밍)"
date: 2025-02-20 14:15:03 +0900
categories: [Programming, Spring]
tags: [Spring Framework, 객체지향]
math: false
toc: true
pin: true
---

### 인터넷 통신

# `IP(Internet Protocol)`

역할 지정한 IP 주소(IP Address)에 데이터 전달

패킷(Packet)이라는 통신 단위로 데이터 전달

![Screenshot 2024-08-28 at 12.36.07 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/f355978b-0442-4c25-90a7-6c523c368d0d/Screenshot_2024-08-28_at_12.36.07_PM.png)

![**클라이언트 패킷 전달**](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/36f91aac-35b1-4e6d-9fcb-3fef4de254a8/image.png)

**클라이언트 패킷 전달**

![Screenshot 2024-08-28 at 12.18.30 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/78886df2-7708-4ae3-8767-c8e3c5ec0ef7/Screenshot_2024-08-28_at_12.18.30_PM.png)

![Screenshot 2024-08-28 at 12.18.20 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/dbde3407-e08a-4953-840f-ec171aead3c3/Screenshot_2024-08-28_at_12.18.20_PM.png)

![Screenshot 2024-08-28 at 12.19.50 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/59963b0b-78f9-4b2f-98d8-e8dfd88efc98/Screenshot_2024-08-28_at_12.19.50_PM.png)

IP 프로토콜의 한계

# `TCP, UDP`

![Screenshot 2024-08-28 at 12.55.55 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/c71735bb-fd0e-4ef6-b94f-44f0ddcd26d9/Screenshot_2024-08-28_at_12.55.55_PM.png)

### TCP 특징

전송 제어 프로토콜(Transmission Control Protocol)

![Screenshot 2024-08-28 at 12.39.04 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/88073cb4-07b1-44d8-919e-c08369d75185/Screenshot_2024-08-28_at_12.39.04_PM.png)

- 연결지향 - `TCP 3 way handshake` (가상 연결)
- 데이터 전달 보증
- 순서 보장

- 신뢰할 수 있는 프로토콜
- 현재는 대부분 TCP 사용

### UDP 특징

사용자 데이터그램 프로토콜(User Datagram Protocol)

- 하얀 도화지에 비유(기능이 거의 없음)
- 연결지향 - TCP 3 way handshake X
- 데이터 전달 보증 X
- 순서 보장 X
- 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
- 정리
    - IP와 거의 같다. + PORT +체크섬 정도만 추가
    - 애플리케이션에서 추가 작업 필요

PORT: 하나의 IP에서 여러 애플리케이션이

![Screenshot 2024-08-28 at 12.35.14 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/91b1c567-e10f-4d63-802b-01355707f1c7/Screenshot_2024-08-28_at_12.35.14_PM.png)

![Screenshot 2024-08-28 at 12.36.44 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/9d72749f-7508-465e-9761-c344d094fb38/Screenshot_2024-08-28_at_12.36.44_PM.png)

# `PORT`

# `DNS`

# `HTTP`

HTTP 메시지에 모든 것을 전송

- HTML, TEXT
- IMACE, 음성, 영상, 파일
- JSON, XML (API)
- 거의 모든 형태의 데이터 전송 가능
- 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용

# `웹 서버`

![Screenshot 2024-08-28 at 12.02.29 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/6fae256d-a4a8-48a6-ad47-5562b4122ff1/Screenshot_2024-08-28_at_12.02.29_PM.png)

- HTTP 기반으로 동작
- 정적 리소스 제공, 기타 부가기능
- 정적(파일) HTML, CSS, JS, 이미지, 영상
    
    예) NGINX, APACHE
    

# `웹 애플리케이션 서버(WAS - Web Application Server)`

- HTTP 기반으로 동작
- 웹 서버 기능 포함+ (정적 리소스 제공 가능)
- 프로그램 코드를 실행해서 애플리케이션 로직 수행
HTML, HTT API(JSON)
- 서블릿, JSP, 스프링 MVC
- 예) 톰캣(Tomcat) Jetty, Undertow

![Screenshot 2024-08-28 at 1.15.03 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/6ccd9ee4-b164-40dc-b294-759288107439/Screenshot_2024-08-28_at_1.15.03_PM.png)

# `웹 서버 vs. 웹 애플리케이션 서버(WAS)`

- 웹 서버는 정적 리소스(파일), WAS는 애플리케이션 로직
- 사실은 둘의 용어도 경계도 모호함
- 웹 서버도 프로그램을 실행하는 기능을 포함하기도 함
- 웹 애플리케이션 서버도 웹 서버의 기능을 제공함
- 자바는 서블릿 컨테이너 기능을 제공하면 WAS
- 서블릿 없이 자바코드를 실행하는 서버 프레임워크도 있음
- WAS는 애플리케이션 코드를 실행하는데 더 특화

### 웹 시스템 구성 - WAS, DB

![Screenshot 2024-08-28 at 1.18.19 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/1965f1eb-ffcf-4eae-a7db-8ada55923ce9/Screenshot_2024-08-28_at_1.18.19_PM.png)

- WAS, DB 만으로 시스템 구성 가능
- WAS는 정적 리소스, 애플리케이션 로직 모두 제공 가능

**단점**

- WAS가 너무 많은 역할을 담당, 서버 과부하 우려
- 가장 비싼 애플리케이션 로직이 정적 리소스 때문에 수행이 어려울 수 있음
- WAS 장애시 오류 화면도 노출 불가능

### 웹 시스템 구성 - WEB, WAS, DB

![Screenshot 2024-08-28 at 1.22.45 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/8013c7fa-7172-4f6f-be89-852b2b3ab3d2/Screenshot_2024-08-28_at_1.22.45_PM.png)

- 정적 리소스는 웹 서버가 처리
- 웹 서버는 애플리케이션 로직같은 동적인 처리가 필요하면 WAS에 요청을 위임
- WAS는 중요한 애플리케이션 로직 처리 전담

![Screenshot 2024-08-28 at 1.23.30 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/bab83619-c6e6-4447-8aa1-9673ad84ed35/031c1def-b838-42e7-870d-a75b2b30b855/Screenshot_2024-08-28_at_1.23.30_PM.png)

- 효율적인 리소스 관리
- 정적 리소스가 많이 사용되면 Web 서버 증설
- 애플리케이션 리소스가 많이 사용되면 WAS 증설