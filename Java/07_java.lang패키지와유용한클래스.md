## java.lang패키지
### Object클래스
- protected Object clone() : 객체 자신의 복사본을 반환한다
- public boolean equals(Object obj) : 객체 자신과 객체 obj가 같은 객체인지 알려준다.(같으면 true)
- protected Class getClass() : 객체 자신의 클래스 정보를 담고 있는 Class인스턴스를 반환한다
- public String toString() : 객체 자신의 정보를 문자열로 반환한다
- public void notify() : 객체 자신을 사용하려고 기다리는 쓰레드를 하나만 깨운다
- public void notifyAll() : 객체 자신을 사용하려고 기다리는 모든 쓰레드를 깨운다
- public void wait() / public void wait(long timeout) / public void wait(long timeout, int nanos) : 다른 쓰레드가 notify()나 notifyAll()을 호출할 때까지 현재 쓰레드를 무한히 또는 지정된 시간(timeout, nanos)동안 기다리게 한다.(timeout은 천 분의 1초, nanos는 10^9분의 1초)
   
+ equals(Object obj)
  참조변수의 값으로 판단한다
   
+ clone()
  Object클래스에 정의된 clone()은 단순히 인스턴스변수의 값만 복사하기 때문에 참조타입의 인스턴스 변수가 있는 클래스는 완전한 인스턴스 복제가 이루어지지 않는다
   
+ 공변 반환타입
  오버라이딩할 때 조상 메서드의 반환타입을 자손 클래스의 타입으로 변경을 허용하는 것   
  Point copy = (Point)originals.clone(); => Point copy = original.clone();   
  일반적으로는 배열을 복사할 때, 같은 길이의 새로운 배열을 생성한 다음에 System.arraycopy()를 이용해서 내용을 복사하지만, 이처럼 clone()을 이용해서 간단하게 복사할 수 있다   
  * clone()으로 복제가 가능한 클래스인지 확인하려면 Java API에서 Cloneable을 구현하였는지 확인하면 된다
   
+ 얕은 복사와 깊은 복사
  clone()은 객체에 저장된 값을 그대로 복제할 뿐, 원본가 복제본이 같은 객체를 공유하므로 '얕은 복사(shallow copy)'라고 한다. 얕은 복사에서는 원본을 변경하면 복사본도 영향을 받는다. 반면에 원본이 참조하고 있는 객체까지 복사하는 것을 '깊은 복사(deep coopy)'라고 하며, 깊은 복사에서는 원본과 복사본이 서로 다른 객체를 참조하기 때문에 원본의 변경이 복사본에 영향을 미치지 않는다.
   
+ getClass()
  Class객체는 클래스의 모든 정보를 담고 있으며, 클래스 당 1개만 존재한다. 그리고 클래스 파일이 '클래스 로더'에 의해서 메모리에 올라갈 때, 자동으로 생성된다. 기존에 생성된 클래스 객체가 메모리에 존재하는지 확인하고, 있으면 객체의 참조를 반환하고 없으면 클래스 패스(classpath)에 지정된 경로르 따라서 클래스 파일을 찾는다. 파일 형태로 저장되어 있는 클래스를 읽어서 Class클래스에 정의된 형식으로 변환하는 것이다. 즉, 클래스 파일을 읽어서 사용하기 편한 형태로 저장해 놓은 것이 클래스 객체이다.
   
+ Class객체를 얻는 방법
  ```
    Class cObj = new Card().getClass(); // 생성된 객체로부터 얻는 방법
    Class cObj = Card.class;  // 클래스 리터럴(*.class)로부터 얻는 방법
    Class cObj = Class.forName("Card"); // 클래스 이름으로부터 얻는 방법
  ```
   
### String클래스
String클래스에는 문자열을 저장하기 위해서 문자형 배열 참조변수(char[]) value를 인스턴스 변수로 정의해놓고 있다
+ 문자열의 비교
  문자열을 만들 때는 두 가지 방법, 문자열 리터럴을 지정하는 방법과 String클래스의 생성자를 사용해서 만드는 방법이 있다. 생성자를 이용한 경우에는 new연산자에 의해서 메모리할당이 이루어지기 때문에 항상 새로운 String인스턴스가 생성된다. 그러나 문자열 리터럴은 이미 존재하는 것을 재사용하는 것이다.
   
+ 문자열 리터럴
  자바 소스파일에 포함된 모든 문자열 리터럴은 컴파일 시에 클래스 파일에 저장된다. 같은 내용의 문자열 리터럴은 한번만 저장된다. 클래스 파일에는 소스파일에 포함된 모든 리터럴의 목록이 있다. 해당 클래스 파일이 클래스 로더에 의해 메모리에 올라갈 때, 이 리터럴의 목록에 있는 리터럴들이 JVM내에 있는 '상수 저장소(constant pool)'에 저장된다.
   
+ String클래스의 생성자와 메서드
  - char charAt(int index) : 지정된 위치(index)에 있는 문자를 알려준다
  - int compareTo(String str) : 문자열과 사전순서로 비교한다. 같으면 0을, 사전순으로 이전이면 음수를, 이후면 양수를 반환한다
  - String concat(String str) : 문자열을 뒤에 덧붙인다
  - boolean contains(CharSequence s) : 지정된 문자열이 포함되었는지 검사한다
  - boolean endsWith(String suffix) : 지정된 문자열로 끝나는지 검사한다
  - boolean equals(Object obj) : 매개변수로 받은 문자열과 String인스턴스의 문자열을 비교한다. obj가 String이 아니거나 문자열이 다르면 false를 반환한다
  - boolean equalsIgnoreCase(String str) : 문자열과 String인스턴스의 문자열을 대소문자 구분없이 비교한다
  - int indexOf(int ch) : 주어진 문자가 문자열에 존재하는지 확인하여 위치를 알려준다. 못 찾으면 -1을 반환한다
  - int indexOf(int ch, int pos) : 주어진 문자가 문자열에 존재하는지 지정된 위치부터 확인하여 위치를 알려준다. 못 찾으면 -1을 반환한다
  - int indexOf(String str) : 주어진 문자열이 존재하는지 확인하여 그 위치를 알려준다. 없으면 -1을 반환한다
  - int lastIndexOf(int ch) : 지정된 문자 또는 문자코드를 문자열의 오른쪽 끝에서부터 찾아서 위치를 알려준다. 못 찾으면 -1을 반환한다
  - int length() : 문자열의 길이를 알려준다
  - String replace(CharSequence old, CharSequence nw) : 문자열 중의 문자열(old)를 새로운 문자열(nw)로 바꾼 문자열을 반환한다
  - String[] split(String regex) : 문자열을 지정된 분리자로 나누어 문자열 배열에 담아 반환한다
  - boolean startsWith(String prefix) : 주어진 문자열로 시작하는지 검사한다
  - String substring(int begin) / String(int begin, int end) : 주어진 시작위치부터 끝 위치 범위에 포함된 문자열을 얻는다. 이 때, 시작위치의 문자는 범위에 포함되지만, 끝 위치의 문자는 포함되지 않는다
  - String toLowerCase() : String인스턴스에 저장되어있는 모든 문자열을 소문자로 변환하여 반환한다
  - String to UpperCase() : String인스턴스에 저장되어있는 모든 문자열을 대문자로 변환하여 반환한다
  - String trim() : 문자열의 왼쪽 끝과 오른쪽 끝에 있는 공백을 없앤 결과를 반환한다. 이 때 문자열 중간에 있는 공백은 제거되지 않는다
  - static String valueOf(boolean/int/char/long/float/double/Object) : 지정된 값을 문자열로 변환하여 반환한다. 참조변수의 경우, toString()을 호출한 결과를 반환한다
   
+ join()과 StringJoiner
  join()은 여러 문자열 사이에 구분자를 넣어서 결합한다. java.util.StringJoiner클래스를 상ㅇ해서 문자열을 결합할 수도 있다
   
+ 문자 인코딩 변환
  ```
    byte[] utf8_str = "가".getBytes("UTF-8");  // 문자열을 UTF-8로 변환
    String str = new String(utf8_str, "UTF-8"); // byte배열을 문자열로 변환
  ```
   
+ String.format()
  형식화된 문자열을 만들어내는 간단한 방법   
  String str = String.format("%d 더하기 %d는 %d입니다.", 3, 5, 3+5);
   
+ String을 기본형 값으로 변환
  valueOf() / parseInt()
   
### StringBuffer클래스와 StringBuilder클래스
String클래스는 인스턴스를 생성할 때 지정된 문자열을 변경할 수 없지만 StringBuffer클래스는 변경이 가능하다. 내부적으로 문자열 편집을 위한 버퍼(buffer)를 가지고 있다. StringBuffer인스턴스를 생성할 때는 생성자 StringBuffer(int length)를 사용해서 StringBuffer인스턴스에 저장될 문자열의 길이를 고려하여 충분히 여유있는 크기로 지정하는 것이 좋다. StringBuffer인스턴스를 생성할 때, 버퍼의 크기를 지정해주지 않으면 16개의 문자를 저장할 수 있는 크기의 버퍼를 생성한다.   
StringBuffer클래스는 equals메서드를 오버라이딩하지 안아서 등가비교연산자(==)로 비교한 것과 같은 결과를 얻는다.   
- StringBuffer append(boolean/char/char[]/double/float/int/long/Object/String) : 매개변수로 입력된 값을 문자열로 변환하여 StringBuffer인스턴스가 저장하고 있는 문자열의 뒤에 덧붙인다
- int capacity() : StringBuffer인스턴스의 버퍼크기를 알려준다. length()는 버퍼에 담긴 문자열의 길이를 알려준다
- char charAt(int index) : 지정된 위치에 있는 문자를 반환한다
- StringBuffer delete(int start, int end) : 시작위치부터 끝 위치 사이에 있는 문자를 제거한다. 단, 끝 위치의 문자는 제외
- StringBuffer deleteCharAt(int index) : 지정된 위치의 문자를 제거한다
- StringBuffer insert(int pos, boolean/char/char[]/double/float/int/long/Object/String) : 두 번째 매개변수로 받은 값을 변환하여 지정된 위치에 추가한다. pos는 0부터 시작
- StringBuffer replace(int start, int end, String str) : 지정된 범위의 문자들을 주어진 문자열로 바꾼다. end위치의 문자는 범위에 포함되지 않음
- StringBuffer reverse() : StringBuffer인스턴스에 저장되어 있는 문자열의 순서를 거꾸로 나열한다
- void setLength(int newLength) : 지정된 길이로 문자열의 길이를 변경한다. 길이를 늘리는 경우에 나머지 빈 공간을 널문자 '\u0000'로 채운다
- String toString()
- String substring(int start) / String substring(int start, int end)
   
+ StringBuilder란?
  StringBuffer는 멀티쓰레드에 안전(thread safe)하도록 동기화되어 있다. StringBuilder는 StringBuffer와 완전히 똑같은 기능으로 작성되어 있다.
   
### Math클래스
+ 예외를 발생시키는 메서드
  - int addExact(int x, int y)
  - int subtractExact(int x, int y)
  - int multiplyExact(int x, int y)
  - int incrementExact(int a)
  - int decrementExact(int a)
  - int negateExact(int a)  // -a
  - int toIntExact(long value)  // (int)value - int로의 형변환
  위의 메서드들은 오버플로우가 발생하면, 예외를 발생시킨다
   
+ Math클랫의 메서드
  - static double/float/int/long abs(double/float/int/long) : 주어진 값의 절대값을 반환한다
  - static double ceil(double a) : 주어진 값을 올림하여 반환한다
  - static double floor(double a) : 주어진 값을 버림하여 반환한다
  - static double/float/int/long max/min(double/float/int/long a, double/float/int/long b) : 주어진 두 값을 비교하여 큰/작은 쪽을 반환한다
  - static double random() : 0.0~1.0범위의 임의의 double값을 반환한다(1.0은 범위에 포함되지 않는다)
  - static long round(double/float a) : 소수점 첫째자리에서 반올림한 정수값(long)을 반환한다. 매개변수의 값이 음수인 경우, round()와 rint()의 결과가 다르다는 것에 주의하자
   
+ Number클래스
  BigInteger는 long으로도 다룰 수 없는 큰 범위의 정수를, BigDecimal은 double로도 다룰 수 없는 큰 범위의 부동 소수점수를 처리하기 위한 것
   
+ 오토박싱 & 언박싱(autoboxing & unboxing)
  이제는 기본형과 참조형 간의 덧셈이 가능하다. 컴파일러가 자동으로 변환하는 코드를 넣어주기 때문이다. 기본형 값을 래퍼 클래스의 객체로 자동 변환해주는 것을 '오토박싱'이라고 하고, 반대로 변환하는 것을 언박싱이라고 한다.
   
   
## 유용한 클래스
### java.util.Objects 클래스
객체의 비교나 널 체크(null check)에 유용하다. requireNonNull()은 해당 객체가 널이 아니어야 하는 경우에 사용한다.
- static boolean isNull(Object obj)
- static boolean nonNull(Object obj)
   
- static boolean equals(Object a, Object b)
- static boolean deepEquals(Object a, Object b)
Objects의 equals()는 Object의 equals()와 달리 null검사를 따로 하지 않아도 된다. deepEquals()는 객체를 재귀적으로 비교하기 때문에 다차원 배열의 비교도 가능하다.
   
### java.util.Random 클래스
생성자 Random()은 종자값을 System.currentTimeMillis()로 한다
   
### 정규식(Regular Expression) - java.util.regex패키지
Pattern은 정규식을 정의하는데 사용되고 Matcher는 정규식(패턴)을 데이터와 비교하는 역할을 한다
1. 정규식을 매개변수로 Pattern클래스의 static메서드인 Pattern compile(String regex)을 호출하여 Pattern인스턴스를 얻는다.   
   Pattern p = Pattern.compile("c[a-z]*");
2. 정규식으로 비교할 대상을 매개변수로 Pattern클래스의 Matcher matcher(CharSequence input)를 호출해서 Matcher인스턴스를 얻는다.   
   Matcher m = p.matcher(data[i]);
3. Matcher인스턴스에 boolean matches()를 호출해서 정규식에 부합하는지 확인한다   
   if(m.matches())
    
- c[a-z]* : c로 시작하는 영단어
- c[a-z] : c로 시작하는 두 자리 영단어
- c[a-zA-Z] : C로 시작하는 두 자리 영단어(a~z 또는 A~Z, 즉 대소문자 구분안함)
- c[a-zA-Z0-9] / c\w : c로 시작하고 숫자와 영어로 조합된 두 글자
- .* : 모든 문자열
- c. : c로 시작하는 두 자리 문자열
- c.* : c로 시작하는 모든 문자열(기호포함)
- c\. : c로 일치하는 문자열'.'은 패턴작성에 사용되는 문자이므로 escape문자인'\'를 사용해야한다
- c\d / c[0-9] : c와 숫자로 구성된 두 자리 문자열
- c.*t : c로 시작하고 t로 끝나는 모든 문자열
- [b|c].* / [bc].* / [b-c].* : b 또는 c로 시작하는 문자열
- [^b|c].* / [^bc].* / [^b-c].* : b 또는 c로 시작하지 않는 문자열
- .*a.* : a를 포함하는 모든 문자열(* : 0 또는 그 이상의 문자)
- .*a.+ : a를 포함하는 모든 문자열(+ : 1 또는 그 이상의 문자. '+'는 '*'과는 달리 반드시 하나 이상의 문자가 있어야 하므로 a로 끝나는 단어는 포함되지 않았다)
- [b|c].{2} : b 또는 c로 시작하는 세 자리 문자열.(b 또는 c 다음에 두 자리이므로 모두 세 자리)
   
정규식의 일부를 괄호로 나누어 묶어서 그룹화(grouping)할 수 있다   
   
* 0\\d{1, 2} : 0으로 시작하는 최소 2자리 최대 3자리 숫자(0포함)
* \\d{3, 4} : 최소 3자리 최대 4자리의 숫자
* \\d{4} : 4자리의 숫자
   
find()는 주어진 소스 내에서 패턴과 일치하는 부분을 찾아내면 true를 반환하고 찾지 못하면 false를 반환한다. find()를 호출해서 패턴과 일치하는 부분을 찾아낸 다음, 다시 find()를 호출하면 이전에 발견한 패턴과 일치하는 부분의 다음부터 다시 패턴매칭을 시작한다. Matcher의 find()로 정규식과 일치하는 부분을 찾으면, 그 위치를 start()와 end()로 알아낼 수 있다.
   
### java.util.Scanner클래스
Scanner는 화면, 파일, 문자열과 같은 입력소스로부터 문자데이터를 읽어오는데 도움을 줄 목적으로 추가되었다
   
### java.util.StringTokenizer클래스
StringTokenizer는 긴 문자열을 지정된 구분자(delimiter)를 기준으로 토큰이라는 여러 개의 문자열로 잘라내는 데 사용된다. StringTokenizer는 구분자로 단 하나의 문자밖에 사용하지 못한다.
- StringTokenizer(String str, String delim) : 문자열을 지정된 구분자로 나누는 StringTokenizer를 생성한다(구분자는 토큰으로 간주되지 않음)
- StingTokenizer(String str, String delim, boolean returnDelims) : 문자열을 지정된 구분자로 나누는 StringTokenizer를 생성한다. returnDelims의 값을 true로 하면 구분자도 토큰으로 간주된다
- int countTokens() : 전체 토큰의 수를 반환한다
- boolean hasMoreTokens() : 토큰이 남아있는지 알려준다
- String nextToken() : 다음 토큰을 반환한다
split()은 빈 문자열도 토큰으로 인식하는 반면 StringTokenizer는 빈 문자열을 토큰으로 인식하지 않기 때문에 인식하는 토큰의 개수가 서로 다른 것을 알 수 있다. split()은 데이터를 큰 토큰으로 잘라낸 결과를 배열에 담아서 반환하기 때문에 데이터를 토큰으로 바로바로 잘라서 반환하는 StringTokenizer보다 성능이 떨어질 수밖에 없다.
   
### java.math.BigInteger클래스
BigInteger는 내부적으로 int배열을 새용해서 값을 다룬다   
- final int signum; // 부호. 1(양수), 0, -1(음수) 셋 중의 하나
- final int[] mag;  // 값
BigInteger는 불변이므로, 반환타입이 BigInteger란 얘기는 새로운 인스턴스가 반환된다는 뜻이다
   
- boolean testBit(int n)  // 우측에서 n+1번째 비트가 1이면 true, 0이면 false
정수가 짝수인지 확인할 때, 정수를 2로 나머지 연산한 결과가 0인지 확인하는 조건식을 작성하였었는데, BigInteger의 경우에도 같은 식으로 작성하면 꽤 복잡해진다. 대신 짝수는 제일 오른쪽 비트가 0일 것이므로, testBit(0)으로 마지막 비트를 확인하는 것이 더 효율적이다. 이처럼 가능하면 산술연산 대신 비트연산으로 처리하도록 노력해야 한다.
   
### java.math.BigDecimal클래스
BigDecimal은 실수형과 달리 정수를 이용해서 실수를 표현한다. 실수를 정수와 10의 제곱의 곱으로 표현한다.   
- 정수 * 10^(-scale)
scale은 0부터 Integer.MAX_VALUE사이의 범위에 있는 값이다. 그리고 BigDecimal은 정수를 저장하는데 BigInteger를 사용한다. 한 가지 주의할 점은, double타입의 값을 매개변수로 갖는 생성자를 사용하면 오차가 발생할 수 있다는 것이다.
   
+ BigDecimal의 연산
  연산결과의 정수, 지수, 정밀도가 달라질 수 있다
   
+ scale의 변경
  BigDecimal을 10으로 곱하거나 나누는 대신 scale의 값을 변경함으로써 같은 결과를 얻을 수 있다. setScale()로 scale값을 줄이는 것은 10의 n제곱으로 나누는 것과 같으므로, divide()를 호출할 때처럼 오차가 발생할 수 있고 반올림 모드를 지정해주어야 한다.
 
