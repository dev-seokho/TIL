# 문자 찾기

## 설명

한 개의 문자열을 입력받고, 특정 문자를 입력받아 해당 특정문자가 입력받은 문자열에 몇 개 존재하는지 알아내는 프로그램을 작성하세요.
대소문자를 구분하지 않습니다.문자열의 길이는 100을 넘지 않습니다.

## 입력

첫 줄에 문자열이 주어지고, 두 번째 줄에 문자가 주어진다.

문자열은 영어 알파벳으로만 구성되어 있습니다.

## 출력

첫 줄에 해당 문자의 개수를 출력한다.

## 예시 입력 1

```
Computercooler
c

```

## 예시 출력 1

```
2
```

## 풀이

```java
import java.util.Scanner;

public class Main {
    public int solution(String str, char t){
        int answer = 0;
        str = str.toUpperCase();
        t = Character.toUpperCase(t);

        for(char x :str.toCharArray()) {
            if(x==t) answer++;
        }
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.next();
        char c = kb.next().charAt(0);
        System.out.print(T.solution(str,c));
    }
}
```

## 배운점

- 전위 연산자, 후위 연산자

전위연산자는 다른 연산자를 처리 후에 ++을 처리     
후위연산자는 ++을 처리 후에 다른 연산자를 처리

- Scanner

입력을 받는 Scanner는 util을 상속 받았다.

- toUpperCase()

String객체를 모두 대문자를 바꾸려면 .toUpperCase()를 사용하면 된다.     
Primitive type인 char를 대문자로 바꾸려면 Character.toUpperCase(변수) 를 사용하면 된다.

- .charAt(index)

Scanner객차로 받은 String을 char형으로 가져오고 싶을 때.
