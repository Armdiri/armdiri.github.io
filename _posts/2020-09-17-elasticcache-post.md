---
title:  "ElasticCache(Redis) 제대로 알고 사용하자"
description: "ElasticCache(Redis) 제대로 알고 사용하자"
date: 2020-09-17 15:26:28 -0400
categories: devlopment
sitemap :
  changefreq : daily
  priority : 1.0
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

