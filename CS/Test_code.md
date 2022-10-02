# 단위 테스트 vs 통합 테스트

- 대답
    
    [https://tecoble.techcourse.co.kr/post/2021-05-25-unit-test-vs-integration-test-vs-acceptance-test/](https://tecoble.techcourse.co.kr/post/2021-05-25-unit-test-vs-integration-test-vs-acceptance-test/)
    
    단위테스트 : 단위테스트는 응용프로그램에서 테스트 가능한 가장 작은 소프트웨어 (엄격하게 크기가 정해져 있진 않지만 일반적으로 클래스 또는 메소드 수준)
    
    통합테스트 : 통합테스트는 단위테스트보다 더 큰 동작을 달성하기위해 여러 모듈을 모아 이들이 의도대로 협력하는지 확인하는 것. 즉 개발자가 변경할 수 없는 부분( 외부라이브러리 ) 까지 포함한 테스트(스프링에서는 @SpringBootTest 를 붙혀서 할 수 있음)