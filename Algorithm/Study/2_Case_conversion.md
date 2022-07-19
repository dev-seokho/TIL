# 대소문자 변환

## 설명

대문자와 소문자가 같이 존재하는 문자열을 입력받아 대문자는 소문자로 소문자는 대문자로 변환하여 출력하는 프로그램을 작성하세요.

## 입력

첫 줄에 문자열이 입력된다. 문자열의 길이는 100을 넘지 않습니다.
문자열은 영어 알파벳으로만 구성되어 있습니다.

## 출력

첫 줄에 대문자는 소문자로, 소문자는 대문자로 변환된 문자열을 출력합니다.

## 예시 입력 1

```
StuDY
```

## 예시 출력 1

```
sTUdy
```

## 나의 풀이 (통과)

```java
import java.util.Scanner;
public class Main {
    public String solution(String str){
        char[] arr = new char[str.length()];
        char[] answerCharList = str.toCharArray();

        for(int i=0; i<str.length(); i++) {
            char e;
            if(Character.isUpperCase(answerCharList[i])){
                e = Character.toLowerCase(answerCharList[i]);
            } else{
                e = Character.toUpperCase(answerCharList[i]);
            }
            arr[i] = e;
        }
        String answer = String.valueOf(arr);
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.next();
        System.out.print(T.solution(str));
    }
}
```

## 다른 풀이

```java
import java.util.Scanner;
public class Main {
    public String solution(String str){
        String answer = "";

        for(char x : str.toCharArray()){
            if(Character).isLowerCase(x) answer+=Character.toUpperCase(x);
            else answer+=Character.toLowerCase(x);
        }
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.next();
        System.out.print(T.solution(str));
    }
}
```

## 아스키코드를 활용한 풀이

```java
import java.util.Scanner;
public class Main {
    public String solution(String str){
        String answer = "";

        for(char x : str.toCharArray()){
            if(x>=97 && x<=122) answer+=(char)(x-32);
            else answer+=(char)(x+32);
        }
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.next();
        System.out.print(T.solution(str));
    }
}
```

## 배운점

- 아스키코드

char는 사실 정수형이기 때문에 아스키 코드로 표현 가능하다.
char를 아스키 코드로 표현했을 때, 영어 대문자는 65-90, 영어 소문자는 97-122이다.
그렇기 때문에 소문자에서 32를 빼면 대문자가 된다.
이렇게 연산후에는 정수형으로 바뀌기 때문에 캐스팅을 해줘야하는 것을 잊지말자. 

- String

String객체는 참조자료형중 유일하게 + 연산자가 가능하다는 사실을 잊지말자.

- toString(), String.valueOf()

두 메서드의 차이점은 null 값에 따른 NPE(Null Pointer Exception)의 발생 유무이다.
값이 없다면 toString()은 NPE를 발생시키고 String.valueOf()는 ‘null’이라는 문자열로 처리한다.