# Java 버전별 특징
## Java 8
### Lambda
### Stream
### interface default Method   
기존 interface는 추상 메서드만을 정의할 수 있었는데 default 선언을 통해 method를 미리 정의해둘 수 있다. 또한 정의된 default method는 상속된 class에서 오버라이딩 될 수 있다.
### Optional
### LocalDateTime

## Java 9
### 모듈화(Jigsaw)
기존 java의 jar 패키징을 통해 모듈화를 진행하고 있지만 jar에는 문제점이 존재한다. 우선 Jar Hell이 있는데 복잡한 ClassLoader로 정의되었을 때 JVM 컴파일은 성공하지만 런타임시 ClassNotFonundException을 마주하게 된다는 것이다. 또한 Jar는 생각보다 무겁다.   
그래서 jigsaw라는 새로운 모듈화를 통해 가볍고 복잡하지 않은 java 모듈 시스템을 구축한 것이다. 특히 라즈베리 파이 같은 저사양 컴퓨터에서 잘 실행될 수 있도록 구조를 잡았다고 하니 앞으로 더 범용성이 커질지도 모른다.
### stream: takeWhile, dropWhile, iterate 등 추가
### optional: ifPresentOrElse 추가
### interface: private method 추가
interface에서 private method를 사용한다는 의미는 기존 interface에서 정의된 메서드는 상속받은 class에서 구현해야했다. 아니면 상속 받은 그대로 사용하던지 하지만 private method는 interface 내부에서만 사용하며 상속 받은 class는 해당 메서드를 따로 구현할 수 없는 것이다.
```java
public interface CustomInterface {
     
    public abstract void method1();
     
    public default void method2() {
        method4();  //private method inside default method
        method5();  //static method inside other non-static method
        System.out.println("default method");
    }
     
    public static void method3() {
        method5(); //static method inside other static method
        System.out.println("static method");
    }
     
    private void method4(){
        System.out.println("private method");
    } 
     
    private static void method5(){
        System.out.println("private static method");
    } 
}
 
public class CustomClass implements CustomInterface {
 
    @Override
    public void method1() {
        System.out.println("abstract method");
    }
     
    public static void main(String[] args){
        CustomInterface instance = new CustomClass();
        instance.method1();
        instance.method2();
        CustomInterface.method3();
    }
}
```

## Java 10
### var 추가
### Garbage Collector(GC) 병렬 처리 도입으로 인한 성능 향상
### JVM heap 영역을 시스템 메모리가 아닌 다른 종류의 메모리에도 할당 가능

## Java 11
### LTS
### Oracle JDK와 OpenJDK 통합
### Oracle JDK가 구독형 유료 모델로 전환
### Lambda에 var 사용 가능
### Java 10부터 Java 소스 파일 을 먼저 컴파일 하지 않고도 실행할 수 있다. 스크립팅을 향한 한 걸음: 이전 java는 소스를 컴파일하여 class로 뽑은 후 class를 실행했는데 java를 통해 바로 실행할 수 있게 되었다.

## Java 12
### 유니코드 11 지원
### switch문 확장
```java
//java 12 이전
String time;
switch (weekday) {
	case MONDAY:
	case FRIDAY:
		time = "10:00-18:00";
		break;
	case TUESDAY:
	case THURSDAY:
		time = "10:00-14:00";
		break;
	default:
		time = "휴일";
}
```
```java
//java12 이후
String time = switch (weekday) {
	case MONDAY, FRIDAY -> "10:00-18:00";
	case TUESDAY, THURSDAY -> "10:00-14:00";
	default -> "휴일";
};
```

## Java 13
### 유니코드 12.1 지원
### switch 개선
```java
boolean result = switch (status) {
    case SUBSCRIBER -> true;
    case FREE_TRIAL -> false;
    default -> throw new IllegalArgumentException(*"something is murky!"*);
};
```
### Multi line String
```java
//Java 13 이전
String htmlBeforeJava13 = *"<html>\n"* +
              *"    <body>\n"* +
              *"        <p>Hello, world</p>\n"* +
              *"    </body>\n"* +
              *"</html>\n"*;
```
```java
//Java 13 이후
String htmlWithJava13 = *"""
              <html>
                  <body>
                      <p>Hello, world</p>
                  </body>
              </html>
              """*;
```

## Java 14
### switch 표준화
조건에 해당하는 라벨을 ,로 구분하여 한 줄에 쓸 수 있고, -> 화살표를 통해 처리할 코드를 작성할 수 있다.   
기존 Switch는 반환값이 없었는데, 새로운 Switch는 반환값을 갖는다. 따라서 다음과 같은 표현이 가능하다.
```java
int numLetters = switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> 6;
    case TUESDAY                -> 7;
    default      -> {
      String s = day.toString();
      int result = s.length();
      yield result;
    }
};
```
-> 표현 오른쪽에 오는 처리는 꼭 단일 수행이 아니어도 된다. 이때는 {} 블록을 만들고 그 안에 수행할 코드를 작성하면된다.   
또 Switch 표현에서 사용되는 yield라는 키워드가 생겼다. 새로운 Switch 표현이 처음 나온 Java 12에서는 break value;와 같은 문법으로 해당 기능을 지원했으나 현재 Java 14에서는 yield로 변경되었다.   
yield는 쉽게 말게 함수의 return과 비슷하다고 할 수 있다.   
yield 키워드는 항상 Switch 블록 내부에서만 사용된다.
* yield 키워드는 변수명으로 사용이 가능하다
### instanceof 개선
```java
//Java 14 이전
if (obj instanceof String) {
    String s = (String) obj;
}
```
이전에는 obj를 캐스팅하는 것이 필요했지만
```java
if (obj instanceof String s) {
    System.out.println(s.contains(*"hello"*));
}
```
다음과 같이 개선되었다.
### record 선언 기능 추가
레코드란?   
- 불변(immutable) 데이터 객체를 쉽게 생성할 수 있도록 하는 새로운 유형의 클래스
- JDK14에서 preview로 등장하여 JDK16에서 정식 스펙으로 포함

[기존의 불변 데이터 객체]   
```java
public class Person {
    private final String name;
    private final int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() {
        return name;
    }
    
    public int getAge() {
        return age;
    }
}
```
- 상태(name, age)를 보유하는 불변 객체를 생성하기 위한 많은 코드를 작성함
- 모든 필드에 final을 사용하여 명시적으로 정의
- 필드 값을 모두 포함한 생성자 
- 모든 필드에 대한 접근자 메서드(getter) 
- 상속을 방지하기 위해 클래스 자체를 final로 선언하기도함
- 로깅 출력을 제공하기 위한 toString 재정의
- 두 개의 인스턴스를 비교하기 위한 hashCode, equals 재정의

[레코드를 이용한 불변 객체]
```java
public record Person(String name, int age) {
}
```
- 레코드 클래스를 사용하면 훨씬 간결한 방식으로 동일한 불변 데이터 객체 정의할 수 있음
  + 이름(Person), 헤더(String name, int age), 바디({})
- 파일러는 헤더를 통해 내부 필드를 추론
  + 생성자를 작성하지 않아도 되고 toString, equals, hashCode 메소드에 대한 구현을 자동으로 제공

### NullPointerException 개선
```
author.age = 35;
---
Exception in thread *"main"* java.lang.NullPointerException:
     Cannot assign field *"age"* because *"author"* is null
```
어떤 변수가 null인지 설명한다.

## Java 15
### 스케일링 가능한 낮은 지연의 가비지 컬렉터 추가(ZGC)
### Sealed Classes
한글로 직역하면 봉인된 클래스로 Java에서 자주 사용하던 상속을 제한할 수 있다.
```java
public sealed interface SafetyBelt permits Car, Truck {
    String belt();
}
```
다음과 같이 SfatetyBelt 안전벨트를 선언해놓자.
```java
public final class Car implements SafetyBelt{

    @Override
    public String belt() {
        // TODO Auto-generated method stub
        return null;
    }
    
}
```
```java
public final class Truck implements SafetyBelt{

    @Override
    public String belt() {
        // TODO Auto-generated method stub
        return null;
    }
    
}
```
다음과 같이 안전벨트는 Car와 Truck에서 사용할 수 있도록 허용했고 실제 상속받아서 belt mehtod를 구현한다.   
상속받은 class는 추가 확장을 방지하기 위해 final로 선언한다.   
   
![image](https://github.com/hhytruth/CS-study/assets/28378553/0762565b-ef39-47a0-865f-46a04a6fcc46)   
다음과 같이 다른 class에서 해당 class를 상속하지 못하도록 막아버린다.   
그럼 여기서 만약 오토바이 Vehicle class에 안전벨트를 구현하려고 하면 어떻게 될까?   
   
![image](https://github.com/hhytruth/CS-study/assets/28378553/e5ce380e-8a72-4076-baef-dd7c4ce60d76)   
당연하게도 허용되지 않은 class는 해당 인터페이스를 상속받을 수 없다.
* 인터페이스 이외에 abstract class에서도 사용할 수 있다.
```java
public abstract sealed class Vehicle permits Car, Truck {
	String belt();
}
```

### Nashorn JavaScript Engine 제거: java에서 javaScript를 실행할 수 있었던 Engine

## Java 16
### Unix-Domain Socket Channels 사용 가능 (Mac 및 Windows(10+)에도 지원)

## Java 17
### Java 11 이후 새로운 LTS
### Pattern Matching for switch
```java
public String test(Object obj) {

    return switch(obj) {
      case Integer i -> *"An integer"*;
      case String s -> *"A string"*;
      case Cat c -> *"A Cat"*;
      default -> *"I don't know what it is"*;
    };
}
```
이제 객체를 전달하여 기능을 전환하고 특정 유형을 확인할 수 있다.
### Sealed Classes (Finalized): Java 15에서 제공되었던 Sealed Classes 기능 완료
### Foreign Function & Memory API: Java Native Interface(JNI)를 대체
### Deprecating the Security Manager: Java 1.0 이후로 보안 관리자가 있었는데 현재 사용되지 않으므로 제거될 예정


   
[참고]   
1. https://velog.io/@ililil9482/Java17%EC%9D%84-%EA%B3%A0%EB%A0%A4%ED%95%B4%EC%95%BC%ED%95%A0%EA%B9%8C   
2. https://velog.io/@nunddu/Java-Switch-Expression-in-Java-14   
3. https://scshim.tistory.com/372  
