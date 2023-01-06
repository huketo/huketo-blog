---
title: "Oracle"
date: 2023-01-06T14:46:01+09:00
draft: false
categories:
  - blockchain
tags:
  - Oracle
  - blockchain
---

# 오라클(Oracle)

- 사전적 정의: 신탁, 조언
- 블록체인: 블록체인 밖에 있는 데이터를 블록체인 안으로 가져오는 것을 말한다.

## 오라클 정의

**블록체인 오라클**: 블록체인 오라클은 안전한 **미들웨어**로 블록체인과 데이터 제공자, 웹 API, 기업 백 엔드, 클라우드 제공자, IoT 기기, 전자서명, 결제 시스템, 다른 블록체인 등과 같은 오프체인 시스템 간 커뮤니케이션을 돕는 역할을 합니다.

- **오프체인(off-chain)**: 블록체인 밖/의 데이터
- **온체인(on-chain)**: 블록체인 안/의 데이터

_전제_: 블록체인 안의 데이터들은 신뢰성을 가지고 있는 무결한 데이터야한다. ← 온체인 내에서는 데이터 위변조가 불가능하기 때문

하지만 블록체인에 넣는 데이터들의 신뢰성을 보장할 수 없기 때문에 생기는 문제 ← 오프체인에서 데이터 위변조에 대한 문제가 해결되지 못했기 때문에 온체인의 데이터를 신뢰하지 못하게 됨

→ 기존의 중앙화된 시스템에선 중앙에 대한 신뢰를 전제로 이루어져왔음

오라클 문제란 오프체인의 데이터가 온체인으로 올때 오프체인의 데이터에 대한 데이터 무결성이 지켜지지 못할때 생김

- 하드웨어: 센서, 장비 오류 등
- 소프트웨어: 데이터수집 봇, 빅데이터분석기, 인공지능 등
- 악의적인 데이터

## 오라클의 주요 기능

- **요청 확인(Listen)** – 블록체인 네트워크를 모니터링해 오프체인 데이터를 요청하는 유저 또는 스마트 컨트랙트가 있는지 확인

- **추출(Extract)** – 서드파티 웹 서버에서 호스팅 되는 오프체인 API와 같은 하나 또는 다수의 외부 시스템으로부터 데이터 가져오기

- **포맷(Format)** – API로부터 받은 데이터를 블록체인이 읽을 수 있는 형태(인풋)로 포맷 또는 블록체인 데이터가 외부 API(아웃풋)에 호환될 수 있도록 상호 시스템 간 커뮤니케이션을 가능하게 함

- **입증(Validate)** – 데이터 서명, 블록체인 트랜잭션 서명, TLS 서명, TEE 실행, 영지식증명 등 다양한 조합을 활용해 오라클 서비스의 퍼포먼스를 증명할 수 있는 암호학적 증거 생성

- **계산(Compute)** – 오라클이 제출한 다수의 데이터에 대한 중간값 계산 또는 개인 리스크 프로필, 시장 시세, 자본 비용 등과 같은 다른 종류의 데이터로부터 보험료 산정하는 더 복잡한 계산을 포함해 데이터에 대한 다양한 종류의 계산 수행

- **전파(Broadcast)** – 컨트랙트를 위한 데이터 및 해당 온체인 증거를 전송하기 위해 블록체인의 트랜잭션을 서명 및 전파

- **아웃풋(Output)** (optional) – 스마트 컨트랙트의 실행과 동시에 외부 시스템에 데이터 전송 (전통적 결제 네트워크에 결제 지시 전달 또는 사이버 물리적 시스템에 영향을 미치는 데이터 전달)

## 오라클 문제의 현재의 해결방안

- 투표: 암호화폐 소유자들에게 투표를 받고 사실여부에 따른 인센티브
  - 아토믹스왑: 1:1 토큰 거래, 가치 상정을 투표로 결정
  - 어거: 토토, 예측 결과를 투표로 결정
- 중앙값: 평균값이 왜곡될 경우를 상정하여 중앙값 사용
  - 메이커 토큰: 스테이블 코인, 외부 거래소의 가격의 중앙값을 활용
- 중간자
  - Oraclize: API방식의 오라클 서비스
  - Chainlink: API방식의 오라클 서비스

## Non-Oracle Adapter

### Hyperledger Fabric의 데이터 처리

> 실행(Execute) → 정렬(Order) → 검증(Validation)

- **블록체인의 Tx 실행 결과는 상호 검증 가능해야 함**

  - Hyperledger Fabric: **각 Endorsing Peer의 Tx 실행결과가 (모두) 일치해야 함**
  - Ethereum: 마이닝 노드가 생성한 블록 안에 있는 Tx와 검증 노드의 Tx 재실행 결과가 일치해야함

- 특정 기관(Oracle 서비스)에 의존하는 (중앙화된) 처리 방식을 배제
  1. 모든 API Call은 정족수 이상의 요청이 있을 때만 외부에 전달
  2. 특정 API Call의 (서명된) 실행 결과는 요청한 각 노드애 전달

1. 실행에서 정렬단계로 넘어갈때 Endorsing Peer의 보증단계를 거쳐야만 정렬단계로 넘어감.
2. 체인코드에 외부 API Call하는 걸 넣었을 때 실행단계에서 API Call이 노드 수 만큼 발생함. 이때 Proxy Server와 연결을 유지하고 있음
3. 중간에 Proxy Server를 두고 Organization수만큼의 API Call이 확인되었을 때 실제로 API Call을 한번만 실행.
4. Proxy Server는 API 결과값을 반환 받고 세션이 유지되어 있는 노드에 API 결과값 반환
5. 노드들의 Tx 실행이 종료되고 Endorsing Peer에 Tx 실행결과를 전달.
6. Endorsing Peer는 모든 Tx 실행결과를 확인하고 보증함.
7. 이후 정렬단계와 검증단계를 거쳐서 최종적으로 Ledger에 기록.

장점: 중간자를 안둬도 됨
단점: 패브릭만 됨

## 오라클이 필요한 경우

1. 외부의 데이터를 가져다가 스마트 컨트랙트를 실행할 때  
   ex) 축구 경기 결과를 예측하고 결과에 따른 보상을 줄 때, 서로 가치가 다른 두 토큰을 교환할 때 가치척도를 off-chain 거래소에서 가져올 때

2. 랜덤한 값을 생성할 때  
   블록체인 내의 정보로 난수를 생성할 때 예측가능한 위험성이 있음.  
   ex) 스마트 컨트랙트로 구현한 카지노 Dapp, 블록체인 게임

3. 스마트 컨트랙트를 자동화할 때  
   ex) 경매 기간을 3일로 잡아두고 경매를 3일후에 끝나게 하고 싶을 때 스마트 컨트랙트 자체적으로 경매종료를 실행 할 수 있는 방법이 없음. 외부의 호출이 필요함.

4. Cross-Chain 다른 블록체인 네트워크와 상호작용할 때  
   ex) 중간자로 검증하고 호출함

## Hyperledger Fabric Oracle

> IBM에서 정리한 Hyperledger Fabric에서의 Oracle 아키텍쳐 패턴

### 1. Hosting an oracle on a global channel

![ibm-1](https://developer.ibm.com/developer/default/articles/oracles-common-architectural-patterns-for-fabric/images/figure2.png)

외부데이터를 가져오는 Org가 정해진 틱마다 데이터를 갱신하고 Data Source Org와 통신하는 글로벌 채널을 두고 모든 조직이 이 데이터를 가져다 씀

### 2. Smart contract invokes external, trusted data source as the oracle

![ibm-2](https://developer.ibm.com/developer/default/articles/oracles-common-architectural-patterns-for-fabric/images/figure3.png)

체인코드를 통해서 직접 외부데이터를 가져옴

### 3. Verifiable credential as source of facts

![ibm-3](https://developer.ibm.com/developer/default/articles/oracles-common-architectural-patterns-for-fabric/images/figure4.png)

issuer는 검증 가능한 증명서를 발행하는 Oracle 역할을 하며, 클라이언트 애플리케이션은 스마트 컨트랙트에 입력으로 필요한 것을 요청하고 서명을 확인하는 것으로 신뢰성을 보장. [Verifiable Credentials Data Model](https://www.w3.org/TR/vc-data-model/)

참조: [IBM Hyperledger Fabric Oracle](https://developer.ibm.com/articles/oracles-common-architectural-patterns-for-fabric/),
[Chainlink Oracle](https://blog.chain.link/what-is-the-blockchain-oracle-problem-korean/)
