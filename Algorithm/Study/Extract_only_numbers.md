# 숫자만 추출

## 설명

문자와 숫자가 섞여있는 문자열이 주어지면 그 중 숫자만 추출하여 그 순서대로 자연수를 만듭니다.   
만약 “tge0a1h205er”에서 숫자만 추출하면 0, 1, 2, 0, 5이고 이것을 자연수를 만들면 1205이 됩니다.  
추출하여 만들어지는 자연수는 100,000,000을 넘지 않습니다.  

## 입력

첫 줄에 숫자가 섞인 문자열이 주어집니다. 문자열의 길이는 100을 넘지 않습니다.

## 출력

첫 줄에 자연수를 출력합니다.

## 예시 입력 1

```
g0en2T0s8eSoft

```

## 예시 출력 1

```
208
```

## 풀이 (통과)

```java
import java.util.Scanner;

public class Main{
    public int solution(String s){
        String answer = "";

        for(char c: s.toCharArray()){
            if (Character.isDigit(c)) answer+=c;
        }

        return Integer.valueOf(answer);
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.nextLine();
        System.out.println(T.solution(str));
    }
}
```

## 다른 풀이 (아스키코드 사용)

```java
import java.util.Scanner;

public class Main{
    public int solution(String s){
        int answer = 0;
        for(char x : s.toCharArray()){
            if(x>48 && x<=57) answer=answer*10+(x-48);
        }

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

- Character.isDigit()

해당 함수를 사용해서 문자인지 숫자인지 판별 가능하다.