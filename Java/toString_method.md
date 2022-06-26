# toString() 을 재정의 해야 하는 이유와 객체에 toString() 함수를 사용했을 때 이상한 코드가 나오는 이유

모든 자바 클래스는 java.lang.Object 클래스를 상속 받습니다.
이 클래스 안에는 toString() 이라는 메소드가 있습니다.

toString()은 `getClss().getName() + '@' + Integer.toHexString(hashCode())` 와 같이 구현이 되어있기 때문에 결과값이 원하는 값이 아닐 확률이 높습니다. 

우리가 원하는 toString()의 기능은 문자열로 변환시켜주는 기능이기 때문에, toString을 직접 overriding해서 사용해야합니다.
toString() overriding은 보통 IDE에서 도와줍니다.