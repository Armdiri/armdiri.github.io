---
title:  "Code Convention"
description: ""
date: 2021-04-01 15:26:28 -0400
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

## 기본사항
### 파일이름
자바 파일이름은 포함된 소스의 최상위 클래스 이름과 .java 확장자로 구성

### Encoding
Encoding 은 UTF-8 이 기본이다.

### 공백문자
개행 문자를 제외하고 ASCII  코드 공백문자(0x20)는 소스 파일에서 유일한 공백문자이다.

### ASCII 코드 외의 문자
아스키코드가 아닌 문자는 유니코드 케릭터나 유니코드 이스케이스가 활용
```java
String unitAbbrev = "μs"; // Best
String unitAbbrev = "\u03bcs"; // "μs" 허락되지만 굳이 이렇게?
```

### 이스케이프 되는 특수문자
\b, \t, \n, \f, \r, \”, \’, \\ 에 대해선 octal 방식(\012) 이나 유니코드(\u000a)보단 앞의 방식을 사용한다.


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
### 구현 주석

#### 형식준수
	* 블록 주석  :  /* 내용 */ , 여러 줄의 주석을 작성할 때 사용한다.
	* 한 줄 주석 : /* 내용 */ , 한 줄 주석을 작석할 때 사용한다.
	* 꼬리 주석  : /* 내용 */ , 한 줄 주석을 소스 코드의 뒷부분에 작성할 때 사용한다.
	* 줄 끝 주석 : // 내용    , 한 줄 주석을 소스 코드의 뒷부분 또는 줄의 첫 부분에 작성할 때 사용한다. 

#### 예시
	* 자동 들여쓰기 
```java
public class Book {
  public void read() {
    boolean read = false;
    
    if(condition) {
      /*
       * 들여쓰기 규칙은 다른 명령문과 동일하다 
       */
    }
  }
}
```
	* 빈줄 삽입, 한칸 들여쓰기 - 블록주석
```java
/*
 * 첫 줄에 빈 줄을 삽입하고,
 * 한 칸 들여쓰기를 적용한다.
 */
```
	* 빈줄 삽입, 한칸 들여쓰기 - 한줄주석
```java
public void main(String[] args) {
  /* 한 칸 들여쓰기를 적용한 여기는 메인입니다 */
}
```
	* 불필요한 주석사용 지양
	주석은 반드시 필요한 경우에 간결하고 명료하게 작성한다. 
	불필요한 주석의 남발은 소스 코드를 복잡하게 만든다.

	* 가독성 준수
	주석의 길이를 엄격히 제한하지는 않으나, 가독성을 떨어뜨리지 않도록 간결작성

	* 짧은 주석 사용 준수 - 꼬리 주석
	짧은 주석에는 꼬리 주석을 사용하고, 소스 코드와 간격을 둔다. 
	여러 개의 꼬리 주석에는 동일한 탭(tab) 간격을 적용하여 정렬한다.

	* 여러 줄의 소스 코드 주석 적용 준수 - 줄 끝 주석
	여러 줄의 소스 코드 주석에는 줄 끝 주석을 사용한다. 
	그러나 여러 줄의 주석 작성에는 줄 끝 주석을 사용하지 않고 블록 주석을 사용한다.
```java
// if(condition) {
//  이런 형태가 여러 줄의 소스코드 주석
// }

// 여러 줄의 주석 작성은
// 줄 끝 주석을 사용하지 않는다.

/*
 * 여러 줄의 주석은 줄 끝 주석 보다
 * 블록 주석을 사용한다.
 */
```


### 문서화 주석
#### 형식준수
* /**    :  /** 형식으로 주석의 시작을 표시한다.
* 내용  : /** 형식 이후에는 반드시 새 줄을 삽입한다.
* */  : 주석 내용 이후에는 반드시 새 줄을 삽입한다.
* /* 형식으로 주석의 끝을 표시한다.
* 한 칸 들여쓰기를 사용한다.

#### 예시
* 파일주석

파일 주석은 작성한 클래스 파일의 간략한 정보를 명시하는 문서화 주석으로 파일 이름과 파일 생성일, 저작권(copyright)을 반드시 포함한다. 파일 주석은 Javadoc 으로 출력되지 않으나, 파일의 라이선스와 생성일을 기록하므로 반드시 작성한다.
```java
/*
 * @(#) MostService.java 2016. 12 16
 * Copyright 2019 Corp. All rights Reserved.
 */
```
* 클래스 주석

클래스 주석은 **개발자의 이름과 생성일**을 반드시 포함한다. 양식은 아래 샘플을 참고한다. 특정 클래스를 상속하거나 구현한 구현체의 경우 @link로 해당 클래스를 명시한다. 해당 클래스를 여러명이 개발할 경우 클래스 주석에 @author를 여러줄로 구현한다.
```java
/**
 * 회원 멤버 인증 서비스
 *
 * @author 고주몽 sample@etoos.com // 필수값
 * @author 고길동 sample2@etoos.com // 필수값
 * @since 2019-03-12 // 필수값
 */
public void MostApiService{
  
}
```
* 메소드 주석

주석은 기본적으로 유지보수가 되지 않거나 간단한 메소드라면 주석 작성 여부를 개발자 본인의 판단에 맡긴다. 메소드 그 자체로 리더빌러티(readability)가 보장된다면 주석을 작성하지 않아도 된다. 필요시 리턴 값, 파라미터, 예외처리 정보를 포함한다. 메소드를 오버라이드한 경우에는 상위 메소드의 레퍼런스를 포함한다. 또한 @author는 메소드 주석이 아니라 해당 클래스 주석에 포함한다.
```java
/**
 * 회원가입
 *
 * @param memberRequest
 * @param serviceCode
 * @throws Exception
 * @see com.?.?....
 */
public void addMember(MemberRequest memberRequest, int serviceCode) throws Exception {
  
}
```
* 인터페이스 메소드
```java
    /**
     * 학생의 이름을 조회하는 메소드 // 필수값
     *
     * @param no 학생 고유 번호 // 필수값
     * @param schoolNo 학생 소속 학교 번호 // 필수값
     * @return 학생 이름 // 필수값
     * @throws NoClassDefFoundError CommonExceptionHandler를 통해 처리// 필수값
     * @since 1.0.0
     */
    public String sampleMethod(int no, int schoolNo) throws NoClassDefFoundError;
```
* 주석내용, 태그 시작구분
```java
/**
 * 필터링을 위한 상수이다. (주석 내용)
 * 빈 줄을 사용하여 구분한다.
 *
 * @see System.getProperty(@ 태그 시작)
 */

public final static String LINE_SEPARATOR = System.getProperty("line.separator");
```
* Getter, Setter, Private 접근 제어자 메소드 주석 사용안함

## 코드작성 규칙

### 들여쓰기
들여쓰기 탭간격은 공백 4자리로 한다.

#### 자동 들여쓰기 사용
```java
import java.io.BufferedReader;
import java.io.IOException;

/**
* 들여쓰기 예제를 보여주고 있다.
*/
class Example {
	// 클래스 몸체 내에서 자동 들여쓰기를 한다.
	private int maxLine;
	private BufferedReader text;
	public int getMaxLine() {
		return maxLine;
	}
	
	public int currentLineSize() {
		// 메소드 몸체 내에서 자동 들여쓰기를 한다.
		String line = null;
		int size = 0;
		
		try {
			// 블록 내에서 자동 들여쓰기를 한다.
			while ((line = text.readLine()) != null) {
				size++;
			}
		} catch (IOException e) {
			e.printStackTrace();
		}
		return size;
	}
}
```

### 중괄호
선언 또는 제어문의 시작 중괄호는 BSD스타일이 아닌 K&R스타일로 한다.
```java
// 안좋은 예
public interface Empty
{
	List<Empty> selectList();
}
// 좋은예
public interface Empty {
	List<Empty> selectList();
}
```

### 공백
* 대괄호([ ]), 산괄호(< >), 종료 구분자(;) 앞에 공백을 삽입하지 않는다.
```java
class MyGenericType<S, T extends Element & List> {
    ...
}

int[] array0 = new int[] {};
public String first;
public String second;
```

* 소괄호(( ))는 키워드(if, for, return 등)와 함께 사용하는 경우에만 소괄호(( )) 앞에 공백을 삽입한다.
```java
/* 소괄호는 키워드와 함께 사용하는 경우 소괄호 앞에 공백을 삽입한다. */
if (maxLine > 80) {
    ...
}

/* 소괄호안의 표현식과 소괄호 사이에는 공백은 삽입하지 않는다. */
for (int i = 0; i < maxLine; i++) {
    ...
}

/* 타입 캐스팅에는 공백을 삽입하지 않는다. */
String s = ((String)object);
```

* 콤마(,)는 반드시 뒤에 공백을 삽입한다.
```java
int[] array1 = new int[] {1, 2, 3};
void bar(int x, int y) throws E0, E1 {
    ...
}
```

* 콜론(:)을 레이블(label)에서 사용하는 경우에는 뒤에 공백을 삽입한다. 단, case 문에서 사용하는 경우에는 공백을 삽입하지 않는다. 그 외 사용하는 경우에는 반드시 앞과 뒤에 공백을 삽입한다.
```java
switch (Color) {
    case RED:
        return GREEN;
    case GREEN:
        return BLUE;
    case BLUE:
        return RED;
    default:
        return BLACK;
}

for (String s : names) {
    ...
}
```

* 구분자 세미콜론(;)은 뒤에 공백을 삽입한다.
```java
for (int i = 0; i < array.length; i++) {
    ...
}
```

* 시작 중괄호({)는 앞에 공백을 삽입한다.
```java
class MyClass implements I0, I1, I2 {
    ...
}

if (true) {
    return 1;
} else {
    return 2;
}
```

* 연산자의 앞과 뒤에는 공백을 삽입한다. 단, 단항 연산자와 전위, 후위 연산자에는 앞과 뒤에 공백을 삽입하지 않는다.
```java
List list = new ArrayList();
int a = -4 + -9;
b = a++ / --number;
boolean value = true && false;
int monthSalary = (20 * daySalary) + incentive;
```

### 빈줄
