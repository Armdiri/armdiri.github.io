---
title:  "Naming Convention"
description: ""
date: 2021-04-23 15:26:28 -0400
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
- 네이밍 컨벤션
- naming convention
---

매번 네이밍룰을 보면서 개발을 진행하고 있지만 가끔 잊어버리거나 익숙하지 않아서 나만의 네이밍으로 개발을 진행하다가 코드리뷰때 댓글이 엄청 달렸던 
기억이 있으실겁니다. 아니면 인수인계하거나 협업하실때 말들이 많이 나왔겠죠? 개발전에 네이밍에 대한 기준이나 자료를 먼저 봤더라면 개발이 끝나고 나서 고치는 
일따위는 없었을겁니다. 

> 안녕하세요. 오늘은 네이밍룰에 대해서 포스트해보려고 합니다. 개발을 하시다 보면 변수,메소드,클래스 명을 어떻게 해야 할지 막막해 하시는 경우가 있으실겁니다. 
> 이 경우 누군가 규칙을 정해 주지 않거나 기준이 없다면 아마 개발자 마다 각기다른 네이밍으로 인해서 인수인계할때 큰 문제점이 발생할수 있고 협업도 어려워 질수도 있습니다. 
> 그래서 기준은 아니더라도 보통 네이밍을 어떻게 하는지에 대해서 포스트 해보았습니다. 

## 기본
### 공통네이밍 규칙

#### 단어생략, 약어사용 지양
클래스, 메소드 등의 이름을 작성하는 경우에는 단어를 생략하거나 약어를 사용하지 않는다. 단, HTML, UML 등과 같은 범용적인 약어는 사용할 수 있다. 약어를 사용하는 경우에는 모두 **대문자**로 작성한다.
```java
public void sendSMStoMember() {
   
}
```

#### 한글 발음 사용 지양
클래스, 메소드 등의 이름에는 한글 발음을 그대로 사용하지 않는다.
```java
public class SuNeungService() {
}
```

#### 특수 문자 사용 지양
클래스, 메소드 등의 이름에는 특수 문자를 사용하지 않는다. 단, 상수의 이름에는 단어 구분을 위해 언더스코어를 사용한다.
```java
public class MessageConstants {
	public static final String ERROR_PREFIX = "error.common.";
}
```

#### 상수, 약어 대문자 사용준수
#### 간결성, 명료성 준수
클래스, 메소드 등의 이름에는 이름을 통해 역활과 목적을 알 수 있도록 간결하고 명료하게 작성한다.
```java
public void joinMemberByTeacher(Member member, Teacher teacher) {
	// 누구를 통해 회원가입이 이뤄졌는지를 명시
}
public void addStudentMemberWithMyTeacher() {
	// 멤버의 속성에서 확인할수 있는 학생, 선생님의 속성에서 확인할수 있는 담임여부등을 고려하면 안좋은 네이밍
}
```

### 패키지 네이밍

#### 소문자 사용
패키지는 모두 소문자로만 사용한다.

#### 패키지 이름 형식 준수
패키지 이름은 com.<domain_name>.<service_name>.<service_domain> 형식을 사용한다.
```java
com.domain.member.login
```

#### 레이어별 구조화된 패키지 이름
* Base - <service_domain>
* Business - <service_domain>.service
* Persistence - <service_domain>.dao
* Domain model - <service_domain>.model
* Entity - <service_domain>.entity

### 클래스 이름

#### 명사 사용 준수
클래스 이름은 명사를 사용한다.
```java
// 나쁜 예
public class Insert()
// 좋은 예
public class Book()
```

#### 영어 사용 준수
#### 파스칼 표기법 준수
파스칼 사용방법은 코드컨벤션을 참고해 주세요.

#### 레이어별 구조화된 클래스 이름
* Base - <model_name>  (예 : Exception, Utils)
* Business - <model_name>Service
* Persistence - <model_name>Dao, <model_name>Repository, <model_name>Mapper
* Domain model - <model_name>Model
* Entity - <model_name>
