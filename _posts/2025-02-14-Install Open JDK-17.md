---
title: "Java 개발환경 설정"
date: 2024-02-14 17:00:00 +0900
categories: [Programming, Java]
tags: [Java, 환경변수]
math: true
toc: true
pin: true
---

## Java JDK 17 설치 및 환경 변수 설정

### 1. JDK 17 다운로드

![JDK 17 다운로드](/assets/img/posts/2024-02-14-1.png)

[JDK 17 다운로드 링크](https://jdk.java.net/java-se-ri/17)

### 2. 압축 해제 후 이동

`jdk-17` 폴더를 `C:\Program Files` 로 드래그하여 이동한다.

![JDK 폴더 이동](/assets/img/posts/2024-02-14-2.png)

### 3. 환경 변수 설정

#### 1) `jdk-17/bin` 경로 복사

`C:\Program Files\jdk-17\bin`

#### 2) 시스템 환경 변수 열기

- `Win + R` → `sysdm.cpl ,3` 입력

![윈도우 창](/assets/img/posts/2024-02-14-3.png)

- 시스템 속성 창에서 `환경 변수(N)` 클릭

![환경 변수 창](/assets/img/posts/2024-02-14-4.png)

![환경 변수 편집](/assets/img/posts/2024-02-14-5.png)

#### 3) `Path`에 JDK 경로 추가

- 시스템 변수에서 `Path` 선택 → 편집
- 새로 만들기 → 복사한 경로 붙여넣기

![Path 설정](/assets/img/posts/2024-02-14-6.png)
![Path 설정](/assets/img/posts/2024-02-14-7.png)

#### 4) JAVA_HOME 설정

![Path 설정](/assets/img/posts/2024-02-14-8.png)
![Path 설정](/assets/img/posts/2024-02-14-9.png)
- 변수 이름: `JAVA_HOME`
- 변수 값: `C:\Program Files\jdk-17`

#### 5) 명령 프롬프트 확인

- `Win + R` → `cmd`
- 다음 명령어 입력하여 설치 확인:

``bash
`java -version`
