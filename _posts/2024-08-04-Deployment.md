---
title: "Docker Container"
date: 2024-07-16 17:19:57 +0900
categories: [Deployment]
tags: [CI/CD, Docker]
math: false
toc: true
pin: true
---

# `Docker`

Docker는 개발자가 컨테이너를 구축, 배포, 실행, 업데이트 및 관리할 수 있게 해주는 오픈 소스 플랫폼이다. *컨테이너*는 애플리케이션 소스 코드를 운영 체제(OS) 라이브러리 및 모든 환경에서 해당 코드를 실행하는 데 필요한 종속성과 결합하는 표준화된 실행 가능한 구성 요소이다.

### Container

[컨테이너](https://www.ibm.com/kr-ko/topics/containers)는 Linux 커널에 내장된 프로세스 격리 및 가상화 기능을 통해 작동한다. 이러한 기능에는 프로세스 간에 리소스를 할당하기 위한 *제어 그룹*(Cgroup)과 시스템의 다른 리소스 또는 영역에 대한 프로세스의 액세스 또는 가시성을 제한하기 위한 *네임스페이스*가 포함된다.

이를 통해 여러 애플리케이션 구성 요소가 호스트 운영 체제의 단일 인스턴스 리소스를 공유할 수 있다. 이러한 공유는 하이퍼바이저를 통해 여러 [가상 머신(VM)](https://www.ibm.com/kr-ko/topics/virtual-machines)이 단일 하드웨어 서버의 CPU, 메모리 및 기타 리소스를 공유할 수 있도록 하는 방식과 거의 동일한 방식이다.

결과적으로 컨테이너 기술은 애플리케이션 격리, 비용 효율적인 확장성, 폐기 가능성 등 VM의 모든 기능과 이점과 함께 다음과 같은 중요한 추가 이점을 제공한다.

- 경량화: VM과 달리 컨테이너는 전체 OS 인스턴스 및 하이퍼바이저의 페이로드를 전달하지 않는다. 여기에는 코드를 실행하는 데 필요한 OS 프로세스 및 종속성만 포함된다. 컨테이너 크기는 메가바이트(일부 VM의 경우 기가바이트)로 측정되며, 하드웨어 용량을 더 잘 활용하고 시작 시간이 더 빠르다.
- 개발자 생산성 향상: 컨테이너화된 애플리케이션은 한 번 작성하면 어디서나 실행할 수 있다. 또한 컨테이너는 VM에 비해 더 빠르고 쉽게 배포, 프로비저닝 및 재시작할 수 있다. 이러한 장점 덕분에 [지속적 통합](https://www.ibm.com/kr-ko/topics/continuous-integration) 및 [지속적 전달](https://www.ibm.com/kr-ko/topics/continuous-delivery)(CI/CD) 파이프라인에서 사용하기에 이상적이며 [애자일 및 DevOps 방식](https://www.ibm.com/kr-ko/topics/devops)을 채택하는 개발 팀에 더 적합하다.
- 리소스 효율성 향상: 컨테이너를 사용하면 개발자는 동일한 하드웨어에서 VM을 사용할 때보다 몇 배나 많은 애플리케이션 사본을 실행할 수 있다. 이러한 효율성을 통해 클라우드 지출을 줄일 수 있다.

**도커 명령어**

```shell
docker ps #find containers that running 

docker ps -a #find all containers 

docker rm [container id] #remove one container

docker rm [container id] , [container id] #remove some containers

docker rm `docker ps -a -q` #remove all containers

docker images #find all images

docker rmi [image id] #remove image

docker rmi -f [image id] #remove image and container 

docker rm -f $(docker ps -aq)

docker rmi $(docker images -q)

sudo systemctl start docker #docker demon 실행
```