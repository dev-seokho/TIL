# 회문 문자열

## 설명

앞에서 읽을 때나 뒤에서 읽을 때나 같은 문자열을 회문 문자열이라고 합니다.  
문자열이 입력되면 해당 문자열이 회문 문자열이면 "YES", 회문 문자열이 아니면 “NO"를 출력하는 프로그램을 작성하세요.  
단 회문을 검사할 때 대소문자를 구분하지 않습니다.

## 입력

첫 줄에 길이 100을 넘지 않는 공백이 없는 문자열이 주어집니다.

## 출력

첫 번째 줄에 회문 문자열인지의 결과를 YES 또는 NO로 출력합니다.

## 예시 입력 1

```
gooG

```

## 예시 출력 1

```
YES
```

## 풀이 (통과)

```java
import java.util.Scanner;

class Main {
    public String solution(String str){
        str = str.toLowerCase();
        if(str.equals(new StringBuilder(str).reverse().toString())) return "YES";
        return "NO";
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.next();
        System.out.println(T.solution(str));
    }
}
```

## 다른 풀이(반으로 잘라서 비교)

```jsx
import java.util.Scanner;

class Main {
    public String solution(String str){
        String answer = "YES";
        str = str.toUpperCase();
        int len = str.length();
        
        for(int i=0; i<len/2; i++){
            if(str.charAt(i)!=str.charAt(len-i-1)) return "NO";
        }
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.next();
        System.out.println(T.solution(str));
    }
}
```

## 다른 풀이(equalseIgnoreCase() 사용)

```jsx
import java.util.Scanner;

class Main {
    public String solution(String str){
        String answer = "NO";

        String tmp = new StringBuilder(str).reverse().toString();
        if(str.equalsIgnoreCase(tmp)) answer = "YES";
        
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.next();
        System.out.println(T.solution(str));
    }
}
```

## 배운점

- .equalsIgnoreCase()

.equalsIgnoreCase를 사용하면 대소문자 관계 없이 동등성을 확인할 수 있다.