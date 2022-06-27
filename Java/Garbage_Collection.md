# GC란?

Java에서 객체가 만들어지면 JVM Heap영역에서 메모리를 점유합니다.
사용되지 않는 객체들은 불필요하게 메모리를 점유하고 있는데, 이를 자동으로 관리해주는 기능이 Garbage Collection 입니다.

`Garbage Collection`은 **메모리를 비워주는 동작**입니다.
`Garbage Collector`는 Garbage Collection을 **동작하는 알고리즘**이며, Java를 실행하기전에 옵션을 지정해줄 수 있습니다.

# GC의 동작원리

# GC unreachable, reachability

GC는 Heap 영역에 존재하는 unreachable(아무것도 참조하지 않고 있는)한 객체를 수거합니다.
객체들은 서로 다른 객체를 참조하며 참조 사슬을 이룰 수 있는데, 유효한 참조 여부를 파악하기 위해 언제나 유효한 **최초의 참조**가 있어야 합니다.
이를 객체 참조의 **root set** 이라고 하며, root set으로 부터 시작한 참조 사슬에 속한 객체가 reachable 객체, 무관한 객체가 unreachable 객체입니다.
GC는 이렇게 unreachable 객체를 대상으로 합니다.
이렇게 객체가 Garbage 인지 아닌지 판별하는 개념을 **reachability** 라고 합니다.

# young 영역에 survivor이 2개로 구성되어 있는 이유

# 트래픽이 무지 많이 몰리는 이벤트가 예정되어있을때, young 영역과 old 영역비율은?

# GC의 종류

# JAVA8 default GC
