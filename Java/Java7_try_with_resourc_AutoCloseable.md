# Java7 try-with-resource와 AutoCloseable

## try-with-resource

Java 7 부터는 try-with-resource 라는 기능이 추가되었습니다.  
한국어로 해석하면 “리소스와 함께 처리하는 try문장”입니다.  
try-with-resource를 사용할 때는 이 인터페이스를 구현한 클래스는 별도로 close()를 호출해줄 필요가 없습니다. 이는 finally 문장에서 close()를 처리하기 위해서 코드의 가독성을 떨어지게 할 필요가 없어집니다.

### Before

```java
public void newScanFile(String fileName, String encoding){
	Scanner scanner = null;
	try {
		scanner = new Scanner(new File(filName), encoding);
		System.out.println(scanner.nextLine());
	} catch(IllegalArgumentException | FileNotFoundException | NullPointerException exception) {
		exception.printStackTrace();
	} finally {
		if(scanner!=null) scanner.close();
	}
}
```

### After

```java
public void newScanFile(String fileName, String encoding){
	try (Scanner scanner = new Scanner(new File(filName), encoding)) {
		System.out.println(scanner.nextLine());
	} catch(IllegalArgumentException | FileNotFoundException | NullPointerException exception) {
		exception.printStackTrace();
	}
}
```

이와 같이 try 블록의 시작 부분에 catch처럼 소괄호 안에 필요한 문장을 포함할 수 있으며, try의 소괄호 내에 예외가 발생할 수 있는 객체에서 close()를 이용해 닫아야 할 필요가 있을 때 `AutoCloseable`을 구현한 객체는 finally 문장에서 별도로 처리할 필요가 없습니다.    
만약 소괄호 내에서 두 개의 객체를 생성할 필요가 있을 때는, `;` 를 사용해서 객체를 생성할 수 있습니다.

## AutoCloseable

Java 7에서는 꼭 닫지 않아도 되는 것들이 있는데, `AutoCloseable`이라는 인터페이스를 구현한 클래스들이 바로 그런 것입니다. 이 인터페이스를 구현한 클래스들은 try-with-resource 문장에서 사용할 수 있습니다. 많이 사용하는 클래스 중 AutoCloseable과 관련 있는 클래스들은 다음과 같습니다.

- java.nio.channels.FileLock
- java.beens.XMLEncoder
- java.beans.XMLDecoder
- java.io.ObjectInput
- java.io.ObjectOutput
- java.util.Scanner
- java.sql.Connection
- java.sql.ResultSet
- java.sql.Statement

이 외에도 많은 클래스들이 AutoCloseable 인터페이스를 구현하고 있습니다.

## AutoCloseable이 보여주는 Interface의 다형성

AutoCloseable은 Interface의 다형성을 보여주기도 합니다.  
`다형성(polymorphism): 여러개의 형태를 가질 수 있다는 의미`   
사용자는 우리는 AutoClosable이라는 interface가 어떤 역할을 하는지만 알면 구현 대상(AutoCloseable 을 구현한 클래스들)의 내부 구조를 알 필요가 없이 AutoClosable의 역할을 수행한다는 사실을 알 수 있습니다. 🙂