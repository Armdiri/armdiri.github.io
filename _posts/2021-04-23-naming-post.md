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

#### 도메인 모델 이름 형식 준수
도메인 모델은 엔티티(Entity) 이름과 유사하게 작성한다.
```java
// 엔티티 이름
MEMBER_STATUS

// 클래스 이름
public class MemberStatus{}
```

#### Service, BO, DAO, Repository 클래스 이름 형식 준수
Service, BO, DAO, Repository 등의 클래스를 인터페이스와 구현부로 구분하는 경우에는 구현부 클래스의 이름을 <model_name>Impl 로 한다. I 와 같은 접두어는 사용하지 않는다.
```java
public interface MemberDAO{} // 인터페이스 선언

// 나쁜 예
public class iMemberDAOImplements implements MemberDAO {} // 인터페이스 구현

// 좋은 예
public class MemberDAOImpl implements MemberDAO {} // 인터페이스 구현
```

#### 접두사/접미사 사용준수
* 클래스를 역할, 기능, 성격으로 분리가 가능한 경우와 클래스의 크기가 큰 경우에는 접두사/접미사를 사용하여 레이어별로 클래스를 분리한다.
* 접두사/접미사는 복합 단어가 아닌 단일 단어를 사용하여 작성한다.
```java
public void ImageUploader {};
```

### 메소드 이름
코딩 컨벤션에서는 CRUD 작업과 관련된 메소드 네이밍을 표준으로 두며 그 외 다른 목적을 가진 메소드 네임은 용도에 맞되 일관적인 네이밍으로 한다. ex) uploadImage() / validateModel() / increaseStock / joinMember()

#### 동사 사용 준수
```java
// 나쁜 예
public void payment() {}
 
// 좋은 예
public void pay() {}
public void run() {}
public void delete() {}
```

#### 카멜표기법 준수
복합어 이름은 첫번째 단어를 소문자로 작성하고 두번째 이상의 단어 첫 글자를 대문자로 작성하여 단어를 구분한다.
```java
// 나쁜 예
public int SumStock() {}

// 좋은 에
public boolean removeSalary() {}
```

#### Java Beans 이름 형식 준수
Accessor/Mutator(Getter/Setter) 메소드는 get+맴버변수 이름, set+맴버변수 이름 형식으로 작성 한다.
단, 데이터 타입이 Boolean 인경우에는 get+맴버변수 이름, set+맴버변수이름 형식대신 is+맴버변수 이름형식을 사용한다.
```java
// 나쁜 예
public void setBook(boolean book)
// 좋은 예
public void setBook(Book book)
public boolean isBook(Book book)
```

#### 레이어별 구조화된 클래스 이름
* Presentation / Business
  [Create] add<ModelName> , create<ModelName>
  [Read] get<ModelName>, get<ModelName>s, find<ModelName>, find<ModelName>s
  [Update] update<ModelName>, modify<ModelName>
  [Delete] remove<ModelName>, delete<ModelName>
* Persistence
  [Create] insert<ModelName>
  [Read] select<ModelName>
  [Update] update<ModelName>
  [Delete]  delete<ModelName>

#### 쿼리 성격 준수 - DAO
DAO 메소드 이름은 쿼리의 성격에 따라 insert, select, update, delete 구문과 매핑하여 사용
단, JPA와 QueryDSL과 같은 경우 위 표준에 따르지 않고 각 라이브러리 룰을 따른다.

### 변수이름
#### 카멜표기법 준수
복합어 이름은 첫번째 단어를 소문자로 작성하고 두번째 이상의 단어 첫글자를 대문자로 작성한다.
```java
// 나쁜 예
private String GuestName;
private int booknumber;
private boolean Enabled;

// 좋은 예
private String guestName;
private int bookNumber;
private boolean enabled;
```

#### 간결성, 명료성 준수
변수 이름은 한글자 이상으로 사용 의도를 충분히 알수 있을 만큼 간결하고 명확하게 작성한다. 단, 스코프 내에서의 역활을 충분히 알아볼수 있다면 짧은 변수명도 허용한다.

#### 임시 변수 외 한글자 이름 사용지양
임시 변수는 한글자 이름을 사용한다.

### 상수 이름
상수는 대문자로 작성하고 복합어의 경우 언더스코어를 사용
```java
public final int STATIC_CONSTANT = 100;
public final String CODE_NAME = 'POSTAL_CODE';
```

## 예시
### Controller
#### Request
```java
public class MemberJoinRequest extends CommonJoinRequest {

    @ApiModelProperty(required = true, value = "회원 아이디", example = "etoos123", position = 10)
    @NotNull
    @Pattern(regexp = Regex.MEMBER_ID)
    @Size(min = 1, max = 40)
    private String memberId;

    @ApiModelProperty(required = true, value = "비밀번호", example = "qwer1234!@#$", position = 20)
    @Pattern(regexp = Regex.MEMBER_PASSWORD)
    @NotNull
    private String password;

    @ApiModelProperty(value = "회원 이름", example = "이투스", position = 30)
    private String memberName;

    @ApiModelProperty(value = "이름", example = "투스")
    @JsonIgnore
    private String firstName;

    ...
}
```

#### Response
```java
public class AddressResponse {
    @ApiModelProperty(required = true, notes = "도로명 주소", example = "남부순환로 2547")
    private String roadAddress;

    @ApiModelProperty(required = true, notes = "도로명 주소의 참고항목", example = "이투스 교육")
    private String roadAddressExtra;

    @ApiModelProperty(required = true, notes = "지번 주소", example = "서초동")
    private String jibunAddress;

    @ApiModelProperty(required = true, notes = "관련 지번", example = "123번지")
    private String relatedJibun;

    @ApiModelProperty(required = true, notes = "우편번호", example = "19283")
    private String zipCode;

    ...
}
```

#### ViewModel
```java
public class LectureViewModel {

    @ApiModelProperty(required = true, value = "강의명")
    private String lectureName;

    @ApiModelProperty(required = true, value = "강의 번호")
    private int lectureNo;

    ...
}
```

#### Api Response
```java
public class MemberApiResponse {

    @ApiModelProperty(value = "수강 목록")
    private final List<Lecture> lectures;

    @Getter
    @Builder
    public static class Lecture {

        @ApiModelProperty
        private final int lectureNo;

        @ApiModelProperty("강의명")
        private final String lectureName;

        @ApiModelProperty("강의 홈페이지 URI")
        private final String lectureUri;
    }
}
```

### Business Layer
#### Utils
* 공통으로 사용하는 유틸리티 클래스의 suffix
* 단수형이 아닌 복수형으로 한다

#### Properties
```java
// property file
application.properties

// property class
@ConfigurationProperties(prefix = "aws.s3")
@Getter
@Setter
public class AwsS3Properties {

    private String endpointUrl;
    private String accesskey;
    private String secretKey;
    private String bucketName;
    private String region;
}
```

#### Code
```java
public enum AdminErrorCode implements ErrorCode {
    DUPLICATED_AUTHORITY_GROUP_NAME("A0001"),
    DUPLICATED_ID("A0002"),
    NOT_MATCHED_PASSWORD("A0003"),
    INVALID_ADMIN_STATUS_TO_REGISTER("A0004")

    private final String code;
    ...
}
```

#### Type
```java
public enum ProviderType implements GenericEnum<String>, DisplayEnum {
    NAVER("naver", "common.provider.type.naver", 1, true, "naver"),
    KAKAO("kakao", "common.provider.type.kakao", 2, true, "kakao"),

    ...
}
```

#### Constants
```java
public class MessageConstants {

    public static final String ERROR_PREFIX = "error.common.";
    public static final String MESSAGE_PREFIX = "message.common.";
    ...
}
```

#### Configuration
```java
public class MessageConstants {

    public static final String ERROR_PREFIX = "error.common.";
    public static final String MESSAGE_PREFIX = "message.common.";
    ...
}
```

### Persistence Layer
#### Entity
```java
// domain + suffix
LectureEntity
OrderEntity
MemberEntity

// domain + use + suffix
LecturePeriodEntity
MemberAuthEntity
```

#### Model
```java
public class MemberModel {}
public class LectureModel {}
public class OrderModel {}
```

#### Dao
```java
@Mapper
public interface CouponDao {
  int insertCouponCode(CouponCode couponCode);
}

@Mapper
public interface LectureDao {
  List<Lecture> selectLectureWithSubject(SubjectCode subjectCode);
}
```

#### Repository
```java
public interface LectureRepository extends JpaRepository<Lecture, Serializable> {
    Optional<Lecture> findByLectureNo(int lectureNo);
    ...
}
```