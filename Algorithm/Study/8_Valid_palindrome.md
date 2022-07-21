# 유효한 팰린드롬

## 설명

앞에서 읽을 때나 뒤에서 읽을 때나 같은 문자열을 팰린드롬이라고 합니다.  
문자열이 입력되면 해당 문자열이 팰린드롬이면 "YES", 아니면 “NO"를 출력하는 프로그램을 작성하세요.  
단 회문을 검사할 때 알파벳만 가지고 회문을 검사하며, 대소문자를 구분하지 않습니다.  
알파벳 이외의 문자들의 무시합니다.

## 입력

첫 줄에 길이 100을 넘지 않는 공백이 없는 문자열이 주어집니다.

## 출력

첫 번째 줄에 팰린드롬인지의 결과를 YES 또는 NO로 출력합니다.

## 예시 입력 1

```
found7, time: study; Yduts; emit, 7Dnuof

```

## 예시 출력 1

```
YES
```

## 나의 풀이 (통과)

```java
import java.util.Scanner;

public class Main{
    public String solution(String str){
        String answer = "NO";
        String newStr = "";

        for(char c: str.toCharArray())
            if(('a'<=c && 'z'>=c) || ('A'<=c && 'Z'>=c)) newStr+=c;

        if (newStr.equalsIgnoreCase(new StringBuilder(newStr).reverse().toString())) answer = "YES";

        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.nextLine();
        System.out.println(T.solution(str));
    }
}
```

## 다른 풀이 (정규표현식, replaceAll 사용)

```jsx
import java.util.Scanner;

public class Main{
    public String solution(String s){
        String answer = "NO";
        
        s = s.toUpperCase().replaceAll("[^A-Z]", "");
        String tmp = new StringBuilder(s).reverse().toString();
        if(s.equals(tmp)) answer = "YES";

        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.nextLine();
        System.out.println(T.solution(str));
    }
}
```

## 배운점

- **replaceAll()**

`String replaceAll(String regex, String replacement)` 를 사용해서 원하는 값을 뽑아낼 수 있다.   
[^A-Z] 는 A-Z가 아닌것을 부정(^) 하는 정규표현식이다.

- String

String은 `+` 연산으로 기본형 타입과 합쳐진다. 기본형 타입도 String으로 만들어 버린다.