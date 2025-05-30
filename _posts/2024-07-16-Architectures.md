---
title: "모놀리식 아키텍쳐 vs. 마이크로 서비스 아키텍쳐"
date: 2024-07-16 17:19:57 +0900
categories: [Architecture]
tags: [Monolithic Architecture, MSA]
math: false
toc: true
pin: true
---

# `Monolithic Architecture`

소프트웨어의 모든 구성요소가 한 프로젝트에 통합되어 있는 형태로, 각 서비스들이 강하게 결합되어 하나의 전체 시스템을 이루는 구조이다.

웹 개발을 예로 들면 웹 프로그램을 개발하기 위해 모듈별로 개발을 하고, 개발이 완료된 웹 어플리케이션을 하나의 결과물로 패키징하여 배포되는 형태를 말한다.

웹의 경우 WAR파일로 빌드되어 WAS에 배포하는 형태를 말한다. 주로 소규모 프로젝트에서 사용된다.

하지만 일정 규모 이상의 서비스, 혹은 수백명 이상의 개발자가 투입되는 프로젝트에서 Monolithic Architecture는 한계를 보인다.

1단계 서비스 요청을 받는 부분
2단계 요청을 처리하는 부분
3단계 데이터를 저장하는 부분

### 장점

개발이 상대적으로 간단한 편이며 흐름, 단계별로 설계가 되어서 데이터 정합성을 맞추기가 쉽다. 구조가 간단해서 전체 아키텍처 설계도 빠르다.

### 단점

- **여러 기능이 추가되면 소스코드가 복잡해져서 가독성이 좋지 못하다.**
- **부분 장애가 전체 서비스의 장애로 확대될 수 있다.**
- **부분적인 *Scale-out(여러 server로 나누어 일을 처리하는 방식)이 어렵다.**
    
    Monolithic Architecture에서는 사용되지 않는 다른 모든 서비스가 Scale-out되어야 하기 때문에 부분 Scale-out이 어렵다.
    
- **서비스의 변경이 어렵고, 수정 시 장애의 영향도 파악이 힘들다.**
    
    여러 컴포넌트가 하나의 서비스에 **강하게 결합**되어 있기 때문에 수정에 대한 영향도 파악이 힘들다.
    
- **배포 시간이 오래 걸린다.**
    
    최근 어플리케이션 개발 방법은 CI/CD를 통한 개발부터 배포까지 빠르게 반영하는 추세이다. 그러나 규모가 커짐에 따라 작은 변경에도 높은 수준의 테스트 비용이 발생하기도 하며, 많은 사람이 하나의 시스템을 개발하여 배포하기 때문에 영향을 줄 수 밖에 없다.
    
- **한 Framework와 언어에 종속적이다.**
    
    Spring framework를 사용할 경우, blockchain 연동 모듈을 추가할 때 node.js를 사용하는 것이 일반적이며 강세이다. 그러나 java를 이용하여 해당 모듈을 작성할 수 밖에 없다. 선정했던 framework가 Spring이기 때문이다.
    

클라우드의 빠른 확장성과 유연한 인프라 환경구조에는 부적합하다.

기존의 특정한 물리적인 서버에 서비스를 올리던 on-promise 서버 기반의 Monolithic Architecture에서 이제는 클라우드 환경을 이용하여 서버를 구성하는 MicroService Architecture로 많은 서비스들이 전환되고 있다.

# `마이크로 서비스 아키텍처(Micro Service Architecture)`

애플리케이션을 작은 서비스 단위로 분리하고 느슨하게 결합된 서비스의 모임으로 구조화하는 소프트웨어 아키텍처 스타일이다.

- 전체 시스템을 독립된 작은 서비스 단위로 분리
- 각 서비스를 독립적으로 개발
- 종속성이 낮다

MSA는 API를 통해서만 상호작용할 수 있다. 즉, 마이크로 서비스는 서비스의 end-point(접근점)을 API 형태로 외부에 노출하고, 실질적인 세부 사항은 모두 추상화한다. 내부의 구현 로직, 아키텍처와 프로그래밍 언어, 데이터베이스, 품질 유지 체계와 같은 기술적인 사항들은 서비스 API에 의해 철저하게 가려진다.

서비스의 독립성과 확장성을 통한 효율적인 소프트웨어 개발 및 유지 보수를 위해 사용한다.

따라서 *SOA(Service Oriented Architecture)의 특징을 다수 공통으로 가진다.

*SOA - 대규모 컴퓨터 시스템을 구축할 때의 개념으로, 업무상 일 처리에 해당하는 소프트웨어 기능을 서비스로 판단하고 그 서비스를 네트워크상에 연동하여 시스템 전체를 구축해 가는 방법론이다.

![](https://velog.velcdn.com/images/rachaen/post/bb6208d5-e690-48f6-8a8b-b69b9b04558a/image.png){: width="600" }

## MSA 장단점

### 장점

- **독립적 배포**: 각 서비스를 개별적으로 업데이트하고 배포할 수 있다.
- **유연성**: 독립적인 실행환경에서 작동하므로, 개별 서비스 단위로 최적화된 기술을 사용하기 좋다.
- **가용성과 안정성 향상**: 에러가 해당 서비스 내에서 제한. 하나의 서비스에 문제가 생기더라도 다른 서비스는 계속 정상적으로 작동. 단일 실패 지점 제거
- **다른 데이터베이스를 소유:** 각 서비스에 적합한 데이터베이스를 정의, 소유할 수 있다.

### 단점

- **개발 생산성 필요**
- **데이터 일관성 유지**: 서비스마다 독립된 데이터베이스를 가지므로 전체 시스템에서 데이터 일관성을 유지하기 힘듬
- **마이크로서비스 간 통신**: 서비스 간에 데이터를 주고받는 상황에서 통신과 트랜잭션 관리에 대한 복잡성이 증가.
- **테스트**: 서로 독립적이므로 종속성과 호환성을 확인하기 위해 전체 시스템 테스트를 수행하는 것이 어려움
- **배포**: 여러 서비스를 배포하고 관리해야 하므로 배포 프로세스가 복잡
- **오류 식별의 어려움**