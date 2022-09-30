# Spring singleton

## Spring singleton vs Java singleton

구현하는 주체: Java 싱글톤은 클래스 로더, 스프링 싱글톤은 스프링 컨테이너  
싱글톤의 스코프 : Java 싱글톤은 코드 전체, 스프링 싱글톤은 해당 컨테이너 내부  
Thread Safety : Java 싱글톤은 구현하는 개발자의 로직에 따라, 스프링 싱글톤은 자동으로 Thread safety 보장