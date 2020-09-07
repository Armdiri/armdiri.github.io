---
title:  "S3를 이용한 이미지 서버 구축하기"
description: "S3를 이용한 이미지 서버 구축하기"
date: 2020-09-07 20:26:28 -0400
categories: devlopment
thumbnail: "/assets/images/s3imageserver/2020-09-07-01.png"
sitemap :
  changefreq : daily
  priority : 1.0
---

>안녕하세요. DX혁신부문 학원솔루션개발팀에 이병철입니다. :)
>저희팀에서 기존 Nginx와 EFS로 구성된 이미지서버를 CF와 S3 구성으로 변경하고 이에 문제점들을 해결하기위한 과정을 수행하게 되었습니다.  
>구글링에서 나온 문서를 토대로 구축해서 진행을 해도 되겠지만 기존방식과의 차이점 또는 성능이슈를 분석하고 올바른 길로 가기위해 불필요한? 아닌 필요한 테스트를 좀 해보았습니다.  

## 아키텍처
먼저 팀내에 프론트 아키텍처를 구성해 보고 이 방안이 맞는건지 조심스럽게 접근하기로 했습니다.

![이미지1](/assets/images/s3imageserver/2020-09-07-01.png)



