
# String constant pool

**Java 에서 String 객체를 생성하는 방법**

Java에서 String 객체를 생성하는 방법은 다음과 같습니다.

1. String literal(”) 를 사용해서 선언  `ex) String str = “abcd”`
2. new 연산자를 사용해서 선언 `ex) String str = new String(”abcd”);`

이 때, String literal로 생성한 객체는 내용이 같다면 같은 객체(같은 메모리 주소)입니다.
반대로 new 연산자로 생성한 String 객체는 내용이 같더라도 개별적인 객체 입니다.

이를 검증하는 방법으로는 `==`(같은 객체인지 확인), `.equals()` (같은 내용인지 확인) 하는 방법으로 검증할 수 있습니다.

도대체 왜 String literal로 선언하는 객체는 new 연산자와는 달리 같은 주소값을 가지고 있는 것일까요?
JVM 구조를 보면 이해하기 쉽습니다.

**Java String constant Pool**

보통 객체를 만들게 되면, Heap 영역에 객체가 생성됩니다.
String 역시 객체를 만들게 되면 Heap 영역에 객체가 생성되는데, 이 때 String literal로 생성하게 된다면 Heap 영역 내의 **String constant pool 영역에 생성됩니다.**

이 후 이와 동일한 값을 또다시 String literal로 생성한다면, 새로운 객체를 만드는것이 아닌 String constant pool 영역에 생성되어 있는 객체를 가리키게되며, 이미 생성된 객체를 재사용하게 되는 것입니다.

하지만 new 연산자를 사용하여 String 객체를 생성한다면, String constant pool 영역이 아닌 **Heap 영역에 객체가 재생성됨으로써, 같은 내용이더라도 다른 객체**가 됩니다.
결론적으로 String 객체를 new 연산자를 사용하여 생성하게 된다면, 같은 값이라고 할지라도 다른 객체이기 때문에 String이 가지는 불변성이라는 장점을 가질 수 없습니다.
그렇기 때문에 String을 선언할때는 최대한 String literal(”)을 사용하여야 합니다.