---
title:  "장애 모니터링 만들기 with Grafana,Promtail,Loki"
description: "이전 장애모니터링에 문제점을 해소하기 위해 자체적으로 모니터링 툴을 활용하여 만들어 보았습니다"
date: 2021-03-01 15:26:28 -0400
categories: TechBlog
toc: true
toc_sticky: true
toc_label: "Table of Contents"
sitemap:
changefreq: daily
priority: 1.0
header:
teaser: 
tags:
- grafana
- loki
- promtail
---

이전에 사용화된 모니터링툴들을 보고 있자면 이걸로 장애인지하는데 문제는 없겠지만 장애 포인트가 어디인지를 명확하게 찾아내는데 이슈가 있어 보였습니다. 
자빅스, 스카우트등 무료툴들이 있었지만 많이 부족해 보였고 잘 보지도 않을뿐더러 이전과의 장애인지 상황이 달라지지 않았죠. 그래서 저희는 장애모니터링을 직접 
만들어 보고자 하였습니다. 

> 안녕하세요. 오늘은 장애모니터링을 만드는 법에 대해서 간략하게 설명해 드리고자 합니다.   
> 물론 투입리소스 대비 효과는 만점이어서 많은 개발자들에게 도움이 되었기에 이렇게 글을 올리게 되었습니다. 

