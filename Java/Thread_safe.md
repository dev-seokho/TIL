# Java thread-safe

## ✅ 동시성 문제가 발생하는 이유

멀티 스레딩은 하나의 프로세스 내에서 여러개의 Thread(PC Register, JVM Stack, Native Method Stack)를 가지며 Method area, Heap영역등은 공유합니다.  
Method area와 Heap영역을 공유하기 때문에 프로그래밍시 동시성 문제가 발생할 수 있습니다.  

## ✅ 동시성 문제 해결법

### ✅ Lock 사용 (Synchronized 키워드 사용)

`synchronized` 키워드를 사용해서 스레드 안정성을 보장할 수 있습니다.   
메서드에 `synchronized` 키워드를 붙여서 동기화를 할 수 있고, `synchronized` 블록을 사용하는 방법도 있습니다.   

### ✅ 자료구조 사용

`java.concurrent` 패키지 하위에 존재하는 자료구조인 `Hashtable`, `ConcurrentHashMap` , `Atomiclnteger` , `BlockingQueue` 등을 사용하여 thread-safe하게 구현할 수 있습니다.   
해당 클래스들은 주요 메서드들이 `synchronized` 키워드에 감싸져있고, 이는 동시성을 보장한다는 사실을 알 수 있습니다.   

### ✅ Stack 한정 프로그래밍

Thread는 프로세스에 할당된 자원(Method area, Heap 영역)은 공유하지만, PC Register, JVM Stack, Native Method Stack은 각 스레드마다 별도로 가지고 있습니다.   
스레드가 각자 고유한 스택과 지역변수를 가진다는 특성을 이해하고 사용하면 동시성을 보장하도록 할 수 있습니다.   

### ✅ ThreadLocal 사용

Stack 한정 프로그래밍을 할 때, 지역변수를 사용하는 것은 메서드 스코프를 벗어나는 순간에 변수 참조가 사라집니다. 그렇기 때문에 해당 변수를 다른 곳에서 이용할 수 없는데, `ThreadLocal` 클래스를 사용하면 쓰레드 영역에 변수를 설정할 수 있습니다.   
`ThreadLocal` 클래스를 사용하면 쓰레드 영역에 변수를 설정하게 되고, 해당 쓰레드가 실행하는 모든 코드에서 해당 쓰레드에 설정된 변수 값을 모두 사용할 수 있게 되는 것 입니다.   

### ✅ 불변객체 사용

불변객체란 객체가 선언된 이후로 변경할 수 없는 객체(ex: String)입니다.   
불변객체는 `setter` 메서드가 없고, 생성자가 `private` 로 설정되어 있으며, 멤버변수들을 `final` 로 선언하기 때문에 동시성을 보장하도록 만들 수 있습니다. 만약 가변객체가 있다면, 방어적 복사본을 생성하는 방식으로 동시성을 보장받을 수 있습니다.   

### ✅ AtomicOOO, ConcurrentOOO (CAS 알고리즘, ReentrantLock, volatile)

synchronized는 blocking을 사용하여 멀티 스레드 환경에서 공유 객체를 동기화 하는 키워드입니다.  
bloking에는 성능이슈가 존재합니다. 그래서 non-blocking을 하면서도, 원자성(여러개의 쓰레드가 있을 때 특정 시점에 어떤 메소드를 두 개 이상의 쓰레드가 동시에 호출하지 못하도록 하는 것)을 보장하기 위한 방법이 고안되었는데 그것이 바로 atomic 변수 입니다.  
이때 atomic의 핵심 동작 원리가 바로 CAS(Compare And Swap) 알고리즘입니다.

#### CAS 알고리즘

Compare And Swap 알고리즘을 의미합니다.  
한국어로 번역해보면 비교 그리고 변환 이라고 볼 수 있습니다. 그렇기 때문에 다음과 같은 동작 원리를 가집니다.  

1. 인자로 기존 값, 변경할 값을 전달합니다.
2. 기존 값이 현재 메모리가 가지고 있는 값과 같다면 **변경할 값을 반영하면서 true를 반환**합니다.
3. 기존 값이 현재 메모리가 가지고 있는 값과 다르다면 **변경할 값을 반영하지 않고 false를 반환**합니다.

false를 반환한다면 무한 루프를 구성하여 변경된 값을 읽고 같은 시도를 반복하거나, 다른 작업을 먼저 처리해도 됩니다. 이부분은 개발자가 결정할 수 있습니다. 한마디로 non-blocking이 가능하기 때문에 blocking인 synchronized 키워드를 사용하는 것 보다 성능 상 이점이 있다고 볼 수 있습니다.  

그렇기 때문에 Atomic type이 빠르다고 볼 수 있습니다.  
Atomic type은 CAS 알고리즘으로 원자성을 해결하면서 volatile 키워드로 가시성도 해결해줍니다.  

#### volatile란?

가시성 문제란 스레드가 변경한 값이 메인 메모리에 저장되지 않아서 다른 스레드가 이 값을 볼 수 없는 상황을 말합니다. 이러한 이유는 재배치(reordering) 이라는 현상 때문인데, 재배치 현상은 특정 메소드의 소스코드가 100% 코딩된 순서로 동작하지 않고 재배치 된다는 것입니다. 동기화 기능을 지정하지 않으면 컴파일러나 프로세서, JVM 등이 프로그램 코드가 실행되는 순서를 임의로 바꿔 실행할 수도 있기 때문입니다.

그렇기 때문에 volatile 키워드란 Java 변수를 조작한 후에 메인 메모리에 바로 반영하겠다고 명시하는 키워드 입니다. 
Atomic type에서는 가시성을 해결하기 위해서 volatile 키워드를 사용합니다. (synchronized 키워드는 그 자체로 가시성 해결)

#### ReentrantLock

ReentrantLock은 java Concurrent API에 포함된 명시적인 lock 방법입니다.  
암시적 lock인 synchronized 키워드와는 다르게 lock과 unlock을 사용해서 시작과 끝을 명확히 할 수 있습니다.  
명시적락은 try 문에서 예외가 발생하면 락이 해제 되지 않는 경우가 발생하는데, 따라서 락이 해제될 수 있도록 catch, finally 블록에서 락을 해제해야합니다.  

```java
import java.util.concurrent.locks.ReentrantLock;

Lock lock = new ReentrantLock();
lock.lock();
try { // 임계영역
 .
 .
 .
} finally {
    lock.unlock();
}
```

명시적 락은 두종류 락의 설정을 지원합니다. ( 기본은 불공정 )

**공정한 방법**

스레드가 락을 사용하려고 할 때, 해당 락이 이미 사용중이라면 스레드가 대기열 맨 뒤에 위치

**불공정한 방법**

스레드가 락을 사용하려고 할 때, 해당 락이 이미 사용중이라면 스레드는 대기열 맨 뒤에 위치  
스레드가 락을 사용하고자 할 때, 그 순간 락이 해제 된다면 대기열에 스레드가 있더라도 락을 확보


즉 불공정한 방법을 사용하는 경우 순서 뛰어넘기가 일어나기도 합니다. (대기자 목록을 뛰어 넘어 락을 확보)
공정한 방법보다 불공정한 방법을 적용하는 것이 성능상의 이점이 크고, 그 이유는 대기 상태에 있던 스레드가 다시 실행 상태로 돌아가고, 실제로 실행되기 까지 상당한 시간이 걸리기 때문입니다.

####  AtomicOOO, ConcurrentOOO (CAS 알고리즘, ReentrantLock, volatile)에 대한 결론

thread safe 보장을 위해 제공하는 기능 중 AtomicOOO, ConcurrentOOO 는 왜 빠른지?  

→ AtomicOOO 는 unblocking을 사용할 수 있는 CAS 알고리즘을 사용하여 동기화 문제를 해결합니다. 그렇기 때문에 blocking인 syncronized 보다 성능이 좋다고 볼 수 있습니다.  

ConcurrenOOO API 에는 ReentrantLock(명시적 락)이 존재합니다.  
이 방법은 공정한 방법과 불공정 방법을 이용할 수 있는데, 불공정 방법을 이용하면 성능상 이득을 볼 수 있습니다.  
또한 ConcurrentHashMap 같은 경우에는 내부적으로 CAS 알고리즘을 쓰기 때문에 성능상 이득을 볼 수 있습니다.

## ✅ 조사를 하며,

동시성 문제가 생기는 이유는 하나의 프로세스에서 여러개의 쓰레드가 하나의 자원을 공유하기 때문에 일어난다고 생각합니다. 결국 Thread-safe를 구현하기 위해서는 **공유하는 자원을 어떻게 처리해 줄것이냐?** 가 관심주제로 이루어졌던 것 같습니다.   

그렇기 때문에 

- 쓰레드들이 순차적으로 공유 자원을 처리하는 방법(Synchronized, CAS 알고리즘 등)으로 충돌이 일어나지 않게하거나,
- 아예 Read-only(불변객체)로 만들어서 공유 자원을 손대지 못하게 하거나,
- 공유하지 않는 자원(Stack)으로만 프로그래밍을 하며 도움을 주는 클래스를 이용하는 것(ThreadLocal Class)

같은 방식으로 활용한다는 생각이 들었습니다. 결국 동시성 문제를 해결하는것도 JVM의 구조와 성질을 잘 알아야 한다고 느꼈습니다.
그리고 이러한 동시성 문제를 해결하는 것에는 뮤텍스, 세마포어, 모니터를 알아두는 것이 도움이 됐습니다. Java는 기본적으로 모니터를 가지고 있으며 synchronized 키워드도 기본적으로 모니터입니다.

* [스레드(or프로세스) 동기화 기법 (Mutex, Spinlock, Semaphore, Monitor)](https://github.com/dev-seokho/TIL/blob/master/CS/Synchronization_techniques.md)