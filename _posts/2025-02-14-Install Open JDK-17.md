---
title: "Java 개발환경 설정"
date: 2024-02-14 17:00:00 +0900
categories: [Programming, Java]
tags: [Java, 설치, 환경변수]
math: true
toc: true
pin: true
---

## Java JDK 17 설치 및 환경 변수 설정

### 1. JDK 17 다운로드

![JDK 17 다운로드](https://file.notion.so/f/f/7982108d-d4ea-4fe1-8e75-807f2dcfe384/8cd171bb-fcf7-43fa-b1ef-eab3abb5705d/image.png?table=block&id=1cf25db8-e7ce-8088-8b20-f150adec45b2&spaceId=7982108d-d4ea-4fe1-8e75-807f2dcfe384&expirationTimestamp=1744156800000&signature=4N85Xz4FOy3dyKaLumumNoIU_EO0QxyHsXPTyODo1Tw&downloadName=image.png)

[JDK 17 다운로드 링크](https://jdk.java.net/java-se-ri/17)

### 2. 압축 해제 후 이동

`jdk-17` 폴더를 `C:\Program Files` 로 드래그하여 이동한다.

![JDK 폴더 이동](https://file.notion.so/f/f/7982108d-d4ea-4fe1-8e75-807f2dcfe384/7484d0b5-f080-4d60-b8c1-9e19a4ec8fef/image.png?table=block&id=1cf25db8-e7ce-80d8-ae35-e6fbbd7b7fec&spaceId=7982108d-d4ea-4fe1-8e75-807f2dcfe384&expirationTimestamp=1744135200000&signature=nFwZXBBPRrwIfXYpWtCvz7hxwAvxhzN9uJqCfDHqojc&downloadName=image.png)

### 3. 환경 변수 설정

#### 1) `jdk-17/bin` 경로 복사

`C:\Program Files\jdk-17\bin`

#### 2) 시스템 환경 변수 열기

- `Win + R` → `sysdm.cpl ,3` 입력

![윈도우 창](https://file.notion.so/f/f/7982108d-d4ea-4fe1-8e75-807f2dcfe384/d4d320c5-8b99-4054-8bd1-17d9352cee8d/image.png?table=block&id=1cf25db8-e7ce-80a8-b7c4-d1d06eba7d04&spaceId=7982108d-d4ea-4fe1-8e75-807f2dcfe384&expirationTimestamp=1744135200000&signature=411Bj1dqqjhPcHbBDCi1gIbeHCvW640GBQxl3z-9HP8&downloadName=image.png)

- 시스템 속성 창에서 `환경 변수(N)` 클릭

![환경 변수 창](https://file.notion.so/f/f/7982108d-d4ea-4fe1-8e75-807f2dcfe384/9f4bc212-06c5-4c61-8a79-21d24413952d/image.png?table=block&id=1cf25db8-e7ce-8032-9a4f-eddff61913a4&spaceId=7982108d-d4ea-4fe1-8e75-807f2dcfe384&expirationTimestamp=1744135200000&signature=2uQ35bjeRHFQ0EbKjlxlgFSSAxChgdQcp-9c1T8reuI&downloadName=image.png)

![환경 변수 편집](https://file.notion.so/f/f/7982108d-d4ea-4fe1-8e75-807f2dcfe384/c9f0c96a-4d4e-4600-a5fc-4cc792273a51/image.png?table=block&id=1cf25db8-e7ce-8085-8ad1-dba761396461&spaceId=7982108d-d4ea-4fe1-8e75-807f2dcfe384&expirationTimestamp=1744135200000&signature=nZuCoVHhFF9kFh8gQPf2lwgvLOoFTSiquXUEZ8czMLI&downloadName=image.png)

#### 3) `Path`에 JDK 경로 추가

- 시스템 변수에서 `Path` 선택 → 편집
- 새로 만들기 → 복사한 경로 붙여넣기

![Path 설정](https://file.notion.so/f/f/7982108d-d4ea-4fe1-8e75-807f2dcfe384/47744e1a-4939-48d4-886d-1058e888e85a/image.png?table=block&id=1cf25db8-e7ce-80fc-98f2-ecc7884d069a&spaceId=7982108d-d4ea-4fe1-8e75-807f2dcfe384&expirationTimestamp=1744135200000&signature=kXiLSkLLFqee391n_cGyxcMv8y2vnsjFu-JV7Ls94sw&downloadName=image.png)

#### 4) JAVA_HOME 설정

- 변수 이름: `JAVA_HOME`
- 변수 값: `C:\Program Files\jdk-17`

#### 5) 명령 프롬프트 확인

- `Win + R` → `cmd`
- 다음 명령어 입력하여 설치 확인:

``bash
`java -version`
