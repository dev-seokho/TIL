# Java에서 == 와 equals의 차이점 그리고 equals를 재선언할 때 hashcode도 재선언해야하는 이유

## == vs equals
- ==
    `==` 연산자는 **동일성 비교**입니다. 객체 인스턴스의 주소값을 비교합니다.
    primitive data type의 경우 ==를 통해 값 비교가 가능합니다.

    primitive 타입이 == 를 사용해서 값 비교가 가능한 이유는 다음과 같습니다.

    -> 변수를 선언하면 Java Runtime Data Area의 Stack 영역에 저장이 되고, 상수는 Runtime Constant Pool에 저장이 됩니다.
    Stack의 변수 선언부는 Runtime Constant Pool의 주소값을 가리키게 되고, 다른 변수도 같은 상수를 저장하게 된다면 같은 Runtime Constant Pool의 주소값을 가리키게 됩니다.

    그렇기 때문에 primitive type의 주소값 비교가 가능 한 것입니다.

- equals()
    `equals()` 메소드는 **동등성 비교** 입니다.
    객체 내부의 실제 값을 비교합니다.

## equals는 왜 재정의 해야하고 equals를 재정의하면 왜 hashcode 도 재정의해야할까요?

✅ **equals 를 오버라이딩 해야하는 이유는?**

equals() 메소드는 Object class의 내부 구현을 보면 작동방식을 알 수 있습니다.
내부 구현은 다음과 같이 되어 있습니다.

```java
public boolean equals(Object obj) {
        return this == obj;
    }
```

`==` 는 동일성 비교로 서로의 주소값을 확인합니다. 하지만 equals에게 바라는 것은 동일성 비교가 아닌 동등성 비교이기 때문에 오버라이딩을 통해서 동등성비교로 재선언을 해주어야 합니다.

✅ **hashCode 란?**

hashCode란 **객체를 구분하기 위한 정수값**입니다. (메모리 상에 객체가 저장된 위치인 주소값과는 전혀 다릅니다.)

✅ **hashCode를 오버라이딩 해야하는 이유**

기본적으로 상속받고 있는 **Object의 hashCode() 메소드는 객체의 메모리 번지**를 이용해서 해시코드를 만들기 때문에 객체마다 다른 값을 가지고 있습니다.
객체의 동등성을 비교할 때 hashCode()를 오버라이딩 해야하는 이유가 여기서 나타나는데,  **HashSet, HashMap, HashTable과 같은 Hash 컬렉션을 사용할 때 문제가 발생할 수 있기 때문입니다.**

이것은 Object 클래스 명세에서 알아볼 수 있는데, hashCode에 관한 규약은 다음과 같습니다.
1. equals 가 사용하는 정보가 변경되지 않는다면 hashcode를 여러 번 호출해도 동일 hash 값을 반환해야 합니다.
2. equals 메소드가 같다고 판단한 두 객체는 같은 hash 값을 반환해야 합니다.
3. equals 메소드가 다르다고 판단한 두 객체의 hash 값이 같을 수는 있습니다, 하지만 이런 일이 자주 일어나면 성능이 떨어집니다.

여기서 2번 규약을 확인해보면 다음과 같은 사실을 알 수 있습니다.
**equals() 객체가 같다고 판단한다면 hashCode() 메소드에서 반환되는 값이 같아야 한다.**

하지만 hashCode는 오버라이딩 전에 객체의 메모리 번지로 해시코드를 만들기 때문에 동등한 객체여도 hash값이 다릅니다.
HashSet, Hashmap, HashTable 같은 Hash 컬렉션은 다음과 같은 알고리즘을 동등한 객체인지 판별합니다.

![hashcode_overriding](../img/hashcode_overriding.png)

hashCode()의 리턴 값이 오버라이딩 전에는 다르기 때문에 equals를 판별하기 전에 다른 객체라고 단정짓게 됩니다.
그렇기 때문에 hashCode()에서 동등한 객체라면 같은 해시값을 리턴하도록 오버라이딩 해주어야합니다.
그리고 오버라이딩은 equals()와 함께 이루어져야 합니다.