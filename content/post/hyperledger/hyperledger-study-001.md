---
title: "Hyperledger Study 001"
date: 2022-12-08T13:41:01+09:00
draft: false
categories:
  - hyperledger
tags:
  - hyperledger-fabric
  - blockchain
---

ledger - 원장, 장부

<br>

개인 또는 기업간 거래를 기록하기 위한 기록물

# 블록체인이란?

배경이나 이런 것을 제외하고 기술적인 측면만 이야기 하자.

<br>

`Blockchain`은 *분산 원장 기술(DLT: Distributed Ledger Technology)*이라고도 불린다.

쉽게 말해 블록(Block)이 데이터(거래내역)를 담는 원장(Ledger)가 될 것이고 이것들이 분산되어 운영되는 데 제 3자의 개입 없이 참여자들이 거래를 진행할 수 있는 네트워크를 형성한 것... 이것이 Chain과 같은 형태로 이어져 있다.

## 블록체인의 구조

1. 합의를 통한 원장 갱신
   블록체인은 여러 참여자가 분산 관리하는 특성 때문에 이 원장을 관리할 때 내용의 일관성을 유지하는 것이 관건이다. 여기서 블록체인은 *합의*라는 구조를 사용하여 원장의 일관성을 유지한다. 합의에는 다양한 방식이 존재한다.

- 퍼블릭 블록체인의 경우

  - 작업증명(PoW, Proof of Work)
  - 지분증명(PoS, Proof of Stake)

- 프라이빗 블록체인의 경우: PBFT(Practical Byzantine Fault Tolerance)

2. 블록체인 원장 개요

3. 스마트 계약
