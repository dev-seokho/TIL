# 단어 뒤집기

## 설명

N개의 단어가 주어지면 각 단어를 뒤집어 출력하는 프로그램을 작성하세요.

## 입력

첫 줄에 자연수 N(3<=N<=20)이 주어집니다.
두 번째 줄부터 N개의 단어가 각 줄에 하나씩 주어집니다. 단어는 영어 알파벳으로만 구성되어 있습니다.

## 출력

N개의 단어를 입력된 순서대로 한 줄에 하나씩 뒤집어서 출력합니다.

## 예시 입력 1

```
3
good
Time
Big

```

## 예시 출력 1

```
doog
emiT
giB

```

## 풀이(통과)

```java
import java.util.Scanner;

public class Main {
    public String[] solution(byte number, String[] inputStringArray){
        String[] array = new String[number];

        for(int i=0; i<number; i++){
            array[i] = new StringBuilder(inputStringArray[i]).reverse().toString();
        }
        return array;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        Byte number = kb.nextByte();
        String inputStringArray[] = new String[number];

        for(int i=0; i<number; i++){
            inputStringArray[i] = kb.next();
        }

        String[] result = T.solution(number, inputStringArray);
        for(String str:result){
            System.out.println(str);
        }
    }
}
```

## 다른 풀이(ArrayList, StringBuilder 사용)

```java
import java.util.Scanner;
import java.util.ArrayList;

class Main {
    public ArrayList<String> solution(int n, String[] str){
        ArrayList<String> answer = new ArrayList<>();
        
        for(String x: str){
            String tmp = new StringBuilder(x).reverse().toString();
            answer.add(tmp);
        }
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        int n = kb.nextInt();
        String[] str = new String[n];
        
        for(int i=0; i<n; i++){
            str[i] = kb.next();
        }
        
        for(String x : T.solution(n, str)){
            System.out.println(x);
        }
    }
}
```

## 다른 풀이(직접 뒤집기)

```java
import java.util.Scanner;
import java.util.ArrayList;

class Main {
    public ArrayList<String> solution(int n, String[] str){
        ArrayList<String> answer = new ArrayList<>();

        for(String x: str){
            char[] s = x.toCharArray();
            int lt=0, rt=x.length()-1;

            while(lt<rt){
                char tmp = s[lt];
                s[lt]=s[rt];
                s[rt]=tmp;
                lt++;
                rt--;
            }
            String tmp = String.valueOf(s);
            answer.add(tmp);
        }
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        int n = kb.nextInt();
        String[] str = new String[n];

        for(int i=0; i<n; i++){
            str[i] = kb.next();
        }

        for(String x : T.solution(n, str)){
            System.out.println(x);
        }
    }
}
```

## 배운점

- StringBuilder

String을 뒤집을 때는 StringBuilder의 .reverse()를 사용할 수 있다.  
ex) `new StringBuilder(x).reverse().toString();`

- 직접 뒤집기

배열을 나열했을 때, 대칭되는 것들끼리 교환해주는 방법으로 직접 reverse 시킬 수 있다.