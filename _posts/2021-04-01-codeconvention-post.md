---
title:  "Code Convention"
description: ""
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
- 코드컨벤션
- code convention
---

개발자가 취업을 하고 나서 맨 처음으로 접하게 되는게 개발조직의 코드컨벤션일것이다. 막상 접하고 나서 잘 안보게 되는데 언젠가는 익숙해 지겠지? 하는 사람들도 있고
개발을 하다가 보면서 하는 사람도 있을것이다. 둘다 방법은 나쁘지 않다고 본다. 처음 접하고 이것을 완벽하게 하는 사람은 없을것이니깐. 
저희도 코드컨벤션을 만들고 모든 개발자가 이렇게 되리라는 생각을 안했다. 그래서 꼭 필요한 항목들만 나열해 보았다. 

> 안녕하세요. 오늘 주제는 코드컨벤션입니다. 이 다음에 네이밍컨벤션까지 하게 되겠지만 먼저 코드컨벤션을 나열해 보려고 합니다. 

## 표기법
표기법에는 헝가리안, 어더스코어, 파스칼, 카멜이 있다. 회사마다 기준이 달라서 4가지 경우를 모두 설명하고 맞게 적용하시면 됩니다. 
저희는 클래스는 파스칼, 변수와 메소드의 경우 카멜을 사용하였습니다. 아래는 표기법의 종류와 예제만을 넣었습니다. 
예제만 보시더라고 내용을 아실걸로 예상되네요. 

### 헝가리안 표기법(Hungarian Notation)
과거 MS에서 많이 사용했지만 현재 닷넷에서도 사용안하는 표기법.
```java
private int intMemberNo;
private String strName;
private boolean bContinue;
```
### 언더스코어 표기법(Underscore Notation)
```java
private List<User> user_data;
private String book_name;
```
### 파스칼 표기법(Pascal Notation)
```java
public class NespressoCoffee{}
public class BookCase{}
```
### 카멜 표기법(Camel Notation)
```java
private String memberName;
private List<Book> soldOutBooks;
private long categoryNo;
```

## 주석

