# GC란 무엇인가요?

Java에서 객체가 만들어지면 JVM Heap영역에서 메모리를 점유합니다.
사용되지 않는 객체들은 불필요하게 메모리를 점유하고 있는데, 이를 자동으로 관리해주는 기능이 Garbage Collection 입니다.

`Garbage Collection`은 **메모리를 비워주는 동작**입니다.
`Garbage Collector`는 Garbage Collection을 **동작하는 알고리즘**이며, Java를 실행하기전에 옵션을 지정해줄 수 있습니다.

# GC의 동작원리는 어떻게 되나요?

# GC 튜닝은 어디서 이루어지나요?

# GC의 종류는 무엇이 있나요?

# GC의 unreachale은 무엇을 뜻하나요?

# GC의 young 영역은 eden과 survivor 2개로 나누어져 있습니다. 이 때 den은 1개 survivor은 2개로 구성되어 있는데요, young 영역에 survivor 는 왜 2개 일까요?

# 트래픽이 무지 많이 몰리는 이벤트가 예정되어있을때, young 영역과 old 영역비율은 어떻게 하는 것이 좋을까요?