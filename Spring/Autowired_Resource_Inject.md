# Autowired, Resource, Inject
세가지의 어노테이션은 의존객체를 찾는 방식이 다르다는 점입니다.  
@Autowired는 스프링이 지원하는 방법으로써 타입→이름→@Qualifier 순서입니다.  
@Resource는 자바가 지원하는 어노테이션으로써 특정 프레임워크에 종속적이지 않으며 이름→타입→@Qualifier 순서입니다.  
@Inject는 자바가 지원하는 어노테이션으로써 특정 프레임워크에 종속적이지 않으며 타입→@Qualifier이름 순서입니다.  
참고로 @Qualifier는 동일한 빈 객체가 여러개 있을 때 한정자를 설정해 줄 수 있습니다.  