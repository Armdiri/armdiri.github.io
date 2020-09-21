---
title:  "ElasticCache(Redis) 제대로 알고 사용하자"
description: "ElasticCache(Redis) 제대로 알고 사용하자"
date: 2020-09-17 15:26:28 -0400
categories: devlopment
sitemap:
  changefreq: daily
  priority: 1.0
cover: /assets/images/elasticcache/2020-09-17-01.png
header:
    overlay_image: /assets/images/elasticcache/2020-09-17-01.png
    caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
---

> 안녕하세요. DX혁신부문 학원솔루션개발팀에 이병철입니다. :)  
> AWS Elastic Cache를 이용하고 있는 도중에 OOM이 발생하는 사건을 계기로 Redis를 좀더 분석해볼필요가 있다라고 판단했습니다.  
> 많은걸 분석할시간이 부족하여 부하테스트 위주로 작업을 진행했습니다. 

## 개요
* Redis Error OOM(Out of memory) 발생
* Session key 저장하면서 TTL 설정이 일부 안된걸로 파악

### 장애 
![이미지1](/assets/images/elasticcache/2020-09-17-01.png)  
![이미지1](/assets/images/elasticcache/2020-09-17-02.png)  
![이미지1](/assets/images/elasticcache/2020-09-17-03.png)  
![이미지1](/assets/images/elasticcache/2020-09-17-04.png)  
![이미지1](/assets/images/elasticcache/2020-09-17-05.png)  

| | 3월4일 (장애시점) | 2월28일 (최대치) | 비고 |
|:---|:---:|:---:|:---:|
|잔여메모리|239M|243M| |
|사용개수| 39,152 | 119,500| |
|캐시사용| 436M | 436M |

~~~~~~~~
* 어플리케이션 로그에 OOM으로 나와서 메모리 사용량을 봐도 3월4일에 239M 여유가 있음. (비교, 2월28일에 최대사용갯수 기준으로 243M 여유)
* 레디스 키발행과 회수에 관한 로직 문제점이 없어 보임. 
* 과도한 스왑사용으로 인한 오류라고 보기엔 스왑범위가 너무 작음 (23M)
~~~~~~~~

> * 메모리가 여유가 있는데 왜 시스템이 멈출까?  
> * 2월28일에 최대로 사용했는데 그때는 문제가 왜 없었지?   
> 
> 위에 두가지 궁금증이 발생했습니다. 그래서 AWS Tam 에게 도움을 요청했고 다음과 같은 답변을 받았습니다. 

## AWS Q&A

~~~~~~~~
1차 문의  
Q : 메모리 여유가 있는데 왜 시스템이 멈췄을까요?
A : 581M 메모리중에 예약메모리 25%를 제외한 436M까지 사용이 가능합니다.  
예약메모리의 경우 새로운 키를 작성하는데 사용하는데 한계에 도달할 경우 예전에 만들어 놓은 키를 제거하거나 TTL이 없는 키를 제거합니다.  
다만 위 전제조건에 일치하는 키가 없을경우 OOM 오류를 반환합니다. 
~~~~~~~~

~~~~~~~~
2차 문의  
Q : CloudWatch 에서 특정인계치에 도달했을경우 Lambda를 이용해서 Flush 하는건 괜찮을까?
A : 권장하지 않음. 모니터링 지표로 보아 T3.medium 권장, MaxMemory-policy 를 검토하여 수치를 조절할것

Q : HA(replica) 구성을 했을경우 Master node에 OOM이 발생했을 경우 Slave node 가 Master node로 승격되어 이행할수 있을까?
A : replica 구조에서 Slave node (승격후)에 쓰기시도시 OOM 발생할수 있음.
~~~~~~~~

### AWS 제안

* Max Memory-policy 정책변경 (volatile-lfu -> allkeys-random)  

| 옵션 | 설명 | 비고 |
|:---:|:---|:---:|
| volatile-lfu |가장 적게 액세스한 키부터 시작해 만료가 <br> 설정된 키 하나를 제거하여 공간 확보|기본|
| allkeys-lru | 최근 사용한 키를 먼저 제거하여 공간 확보 | |
| allkeys-random | 무작위로 키를 제거하여 공간 확보 | 권장 |
| volatile-random | 만료가 설정된 무작위 키를 제거하여 공간 확보 | 권장 |
| allkeys-lfu | 	가장 적게 액세스한 키를 제거하여 공간 확보 |  |

* 예약 메모리 비율 (reserved-memory-percent) 조정(단, 단독구성시 필요없음)
* 데이터 수명주기 정책 (TTL이 만료되어 학제되는 속도 < 데이터쓰기속도 = OOM발생 )

> 이런 설정이 있었는지 처음에 몰라서 문의사항 및 제안 방식에 따라서 써보려고 했습니다.  
> 근데 진짜 저렇게 했을때 이슈가 없을까? 라는 의구심이 들기 시작했죠. 
> 그래서 테스트계획을 하고 테스트 진행을 하기로 했습니다. 

## Test

*Reference*
* https://docs.aws.amazon.com/ko_kr/AmazonElastiCache/latest/red-ug/Replication.Redis.Groups.html
* https://docs.aws.amazon.com/ko_kr/AmazonElastiCache/latest/red-ug/Replication.Redis-RedisCluster.html
* https://aws.amazon.com/ko/premiumsupport/knowledge-center/oom-command-not-allowed-redis/
* https://docs.aws.amazon.com/ko_kr/AmazonElastiCache/latest/red-ug/scaling-redis-cluster-mode-enabled.html
* https://docs.aws.amazon.com/ko_kr/AmazonElastiCache/latest/red-ug/Strategies.html