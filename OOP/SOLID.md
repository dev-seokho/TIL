# SOLID

## SRP

어떠한 클래스를 변경해야 하는 이유는 오직 하나 뿐이어야 한다 - 로버트 C. 마틴

- 소프트웨어를 구성하는 설계부품인 클래스나 함수는 단 하나의 기능만 가져야한다는 의미이다. 어떠한 클래스를 변경하기 위해서는 반드시 바꾸려는 이유가 한가지여야 한다.
- 남자라는 클래스는 여자친구라는 클래스에게 남자친구 역할을, 어머니에게는 아들 역할을, 직장상사에게는 사원역할을 소대장에게는 소대원 역할을 한다. 이 남자라는 클래스는 역할과 잭임이 너무 많다. 이는 단일 책임 원칙을 위배한다. 만약 남자가 여자친구와 헤어진다면 나머지 클래스들에게 영향을 미칠 것이다.
- 단일 책임 원칙과 가장 관계가 깊은 것은 바로 모델링 과정을 담당하는 추상화이다. 애플리케이션의 경계를 정하고 추상화를 통해 클래스들을 선별하고 속성과 메서드를 설계할 때 반드시 단일 책임 원칙을 고려하는 습관을 들여야 한다.

## OCP

소프트웨어 엔티티(클래스, 모듈, 함수 등)은 확장에 대해서는 열려 있어야 하지만 변경에 대해서는 닫혀 있어야 한다. - 로버트 C. 마틴

- 한마디로 표현하면 자신의 확장에는 열려 있고, 주변의 변화에 대해서는 닫혀 있어야 한다.  
- 자바 자체에도 개방 폐쇄 원칙이 적용돼 있다. 자바 개발자는 작성하고 있는 소스코드가 윈도우에서 구동될지, 리눅스에서 구동될지 또는 다른 운영체제에서 구동될지에 대해서 걱정하지 않는다. 각 운영체제별 JVM과 목적 파일(.class)가 있기 때문에 개발자는 자신에게 설치된 JVM에서 구동하는 코드만 작성하면 된다. 개발자가 작성한 소스코드는 운영체제의 변화에 닫혀있고, 각 운영체제별 JVM은 확장에 열려 있는 구조가 된다. 개발자의 소스코드와 운영체제별 JVM 사이에는 목적 파일이라고 하는 완충장치가 있기 때문이다.  이 외에도 자바에는 개방 폐쇄 원칙이 잘 적용 돼 있으며 이 사례는 각종 상속에서 알아볼 수 있다.  
- 개방 폐쇄 원칙을 무시하고 프로그래밍을 작성하면 객체 지향 프로그래밍의 가장 큰 장점인 **유연성, 재사용성, 유지보수성** 등을 얻을 수 없다. 따라서 객체 지향 프로그래밍에서 개방 폐쇄 원칙은 반드시 지켜야할 원칙이다.  
- 스프링 프레임워크는 개방 폐쇄 원칙을 교과서적으로 활용하고 있다.

## LSP

서브 타입은 언제나 자신의 기반 타입(base type)으로 교체할 수 있어야 한다. - 로버트 C. 마틴

- 다음과 같은 문장대로 구현된 프로그램이라면 이미 리스코프 치환 원칙을 잘 지키고 있다고 말할 수 있다.
    - 하위 클래스 is a kind of 상위 클래스 - 하위 분류는 상위 분류의 한 종류이다.
    - 구현 클래스 is able to 인터페이스 - 구현 분류는 인터페이스할 수 있어야 한다.
- 계층도, 조직도(아버지-딸 구조)는 리스코프 치환 원칙을 위배하고 있는 것이며, 분류도(동물-펭귄 구조)는 리스코프 치환원칙을 만족하는 것이다.
- 하위 클래스나 인스턴스는 상위형 객체 참조 변수에 대입해 상위 클래스의 인스턴스 역할을 하는 데 문제가 없어야 한다.
    - 동물 뽀로로 = new 펭귄(); → 맞는 예
    - 아버지 춘향이 = new 딸(); → 틀린 예

## ISP

클라이언트는 자신이 사용하지 않는 메서드에 의존 관계를 맺으면 안된다. - 로버트 C. 마틴

- 단일 책임 원칙에서 제시한 해결책은 남자 클래스를 토막내서 하나의 역할만 하는 다수의 클래스로 분할하는 것이었는데, 이를 원치 않을 때 선택할 수 있는 방법이 바로 ISP, 인터페이스 분리 법칙이다.
- 단일 책임 원칙(SRP)와 인터페이스 분할 원칙(ISP) 는 결론적으로 같은 문제에 대한 두 가지의 다른 해결책이라고 볼 수 있다. 프로젝트의 요구사항과 설계자의 취향에 따라서 단일 책임 원칙이나 인터페이스 분할 원칙 중 하나를 선택해서 설계할 수 있다. 하지만 **특별한 경우가 아니라면 단일 책임 원칙을 적용하는 것이 더 좋은 해결책이 될 수 있다.**
- 상속과 인터페이스를 얘기할 때 상위 클래스는 풍성할수록 좋고, 인터페이스는 작을수록 좋다고 했다. 인터페이스를 통해 메서드를 외부에 제공할때는 최소한의 메서드만 제공하란는 것이다. 남자친구 인터페이스에 사격하기() 메서드를 제공할 필요도 없고 제공해서도 안되는 것이다. 그리고 리스코프 치환 원칙에 따라서 하위 객체는 상위 객체인 척 할 수 있기 때문에 상위 클래스는 풍성할수록 좋다.


## DIP

고차원 모듈은 저차원 모듈에 의존하면 안된다. 이 두 모듈 모두 다른 추상화된 것에 의존해야 한다. 추상화된 것은 구체적인 것에 의존하면 안된다. 구체적인 것이 추상화된 것에 의존해야 한다. 자주 변경되는 구체(Concreate) 클래스에 의존하지 마라. - 로버트 C. 마틴

- 자신보다 변하기 쉬운 것에 의존하던 것을 추상화된 인터페이스나 상위 클래스를 두어 변하기 쉬운 것의 변화에 영향받지 않게 하는 것이 의존 역전 원칙이다. **자신보다 변하기 쉬운것에 의존하지 마라**
- OCP(개방 폐쇄 원칙)을 설명할 때 나온 설명과 비슷한데, 이렇게 하나의 해결책을 찾으면 그 안에 여러 설계 원칙이 녹아 있는 경우가 많다.
- **상위 클래스일수록, 인터페이스일수록, 추상 클래스일수록 변하지 않을 가능성이 높기 때문에 하위클래스나 구체 클래스가 아닌 상위 클래스, 인터페이스, 추상 클래스를 통해 의존하라는 것이 의존 역전의 원칙**이다.