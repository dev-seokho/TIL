# Optional

## Java 8 Optional 은 왜 사용하는걸까요?

Optional 클래스는 Null 처리를 보다 간편하게 하기 위해서 Java 8 부터 만들어졌습니다.   
개발을 할 때 가장 많이 발생하는 예외중 하나가 Null Pointer Exception 이며, 이를 피하기 위해서는 Null 여부를 검사해야하고, Null 여부를 검사하게 되면 코드가 복잡해지고 번거로워집니다. Java 8 부터는 Optional<T> 클래스를 사용해서 이를 보완하면서 Null Pointer Exception 을 방지하도록 도와줍니다.

### Optioanl을 사용하면 좋은 순간

Optional<T> 클래스는 Wrapper 클래스로, 값을 묶고 풀고, Null 일 경우에는 대체하는 함수를 호출하며 오버헤드가 있습니다. 이러한 방식으로 인해서 시스템 성능이 저하될 우려가 있기 때문에 반환 값이 Null이 절대 아니라면 Optional을 사용하지 않는 것이 좋으며, Null에 의한 오류가 발생할 가능성이 높거나 결과가 Null이 될 확률이 높을 때 사용하는 것이 좋습니다.  

## Optional에서 OrElse OrElseGet 차이

Optianl 클래스에 있는 orElse와 orElseGet 함수의 내부를 들여다보면 다음과 같습니다.

```java
public T orElse(T other) {
        return this.value != null ? this.value : other;
    }

public T orElseGet(Supplier<? extends T> supplier) {
        return this.value != null ? this.value : supplier.get();
    }
```

서로 다른 점은 받는 매개변수가 다르다는 것인데, `orElse`는 매개변수로 값을 받는 반면에 `orElseGet`은 `T` 객체를 리턴하는 `Supplier` 함수적 인터페이스를 매개변수로 받고 있습니다.

즉 값을 생성 후 받느냐(`orElse`), 값 생성전에 인터페이스로 받은 뒤 만약 Null이라면 그 때 값을 생성하느냐(`orElseGet`)에 대한 차이가 존재합니다.

`orElse` 는 조회 결과와 무관하게 값으로 넘어간 함수 자체가 실행된 후 값이 전달되기 때문에 값이 미리 존재하는 경우에 사용하며, 값이 미리 존재하지 않는 경우에는  `orElseGet` 을 사용하는 것이 일반적입니다.