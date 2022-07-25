# 가장 짧은 문자거리

## 설명

한 개의 문자열 s와 문자 t가 주어지면 문자열 s의 각 문자가 문자 t와 떨어진 최소거리를 출력하는 프로그램을 작성하세요.

## 입력

첫 번째 줄에 문자열 s와 문자 t가 주어진다. 문자열과 문자는 소문자로만 주어집니다.  
문자열의 길이는 100을 넘지 않는다.

## 출력

첫 번째 줄에 각 문자열 s의 각 문자가 문자 t와 떨어진 거리를 순서대로 출력한다.

## 예시 입력 1

```
teachermode e

```

## 예시 출력 1

```
1 0 1 2 1 0 1 2 2 1 0
```

## 풀이 (일부 통과, 일부 런타임 에러)

```java
import java.util.Scanner;
import java.util.ArrayList;
import java.util.Collections;

public class Main{
    public String solution(String s, char t){
        String answer = "";
        ArrayList<Integer> list = new ArrayList<Integer>();
        char charArray[] = s.toCharArray();

        for(int i=0; i<charArray.length; i++){
            if (charArray[i] == t) list.add(i);
        }

        for(int i=0; i<charArray.length; i++){
            ArrayList<Integer> result = new ArrayList<Integer>();

            for(int j: list){
                result.add(Math.abs(i - j));
            }
            answer = answer + Collections.min(result) + " ";
        }

        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);

        String s = kb.next();
        char t = kb.next().charAt(0);

        System.out.println(T.solution(s, t));
    }
}
```

## 다른 풀이 (왼쪽부터 읽고, 그 다음 오른쪽으로 읽기)

```jsx
import java.util.Scanner;

public class Main{
    public int[] solution(String s, char t){
        int[] answer = new int[s.length()];
        int p = 1000;

        for(int i=0; i<s.length(); i++){
            if(s.charAt(i) == t){
                p = 0;
                answer[i] = p;
            } else {
                p++;
                answer[i] = p;
            }
        }
        p = 1000;
        for(int i=s.length()-1; i>=0; i--){
            if(s.charAt(i) == t) p=0;
            else{
                p++;
                answer[i] = Math.min(answer[i], p);
            }
        }

        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);

        String str = kb.next();
        char t = kb.next().charAt(0);

        for(int x: T.solution(str, t)){
            System.out.print(x+" ");
        }
    }
}
```

## 배운점

- Math함수

Math 함수를 사용해서 두 수의 작은 값도 구할 수 있고, 양수만을 구할수도 있다.

- 길이 구하기

기본형변수 배열의 길이는 length로, String은 length(), ArrayList는 size() 로 구하는등 각각 길이 구하는 방법이 다르다.