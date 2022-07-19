# 문장 속 단어

## 설명

한 개의 문장이 주어지면 그 문장 속에서 가장 긴 단어를 출력하는 프로그램을 작성하세요.
문장속의 각 단어는 공백으로 구분됩니다.

## 입력

첫 줄에 길이가 100을 넘지 않는 한 개의 문장이 주어집니다. 문장은 영어 알파벳으로만 구성되어 있습니다.

## 출력

첫 줄에 가장 긴 단어를 출력한다. 가장 길이가 긴 단어가 여러개일 경우 문장속에서 가장 앞쪽에 위치한 단어를 답으로 합니다.

## 예시 입력 1

```
it is time to study
```

## 예시 출력 1

```
study
```

## 나의 풀이(통과)

```java
import java.util.Scanner;
public class Main {
    public String solution(String str){
        String max = "";
        String[] stringArray = str.split(" ");
        for(String e:stringArray){
            if(max.length() < e.length()) max = e;
        }
        return max;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.nextLine();
        System.out.print(T.solution(str));
    }
}
```

## 다른 풀이 (subString() 과 indexOf()를 사용한 풀이)

```java
import java.util.Scanner;
public class Main {
    public String solution(String str){
        String answer = "";
        int m = Integer.MIN_VALUE, pos;

        while((pos = str.indexOf(' ')) != -1){
            String tmp = str.substring(0, pos);
            int len = tmp.length();
            if(len>m){
                m=len;
                answer=tmp;
            }
            str = str.substring(pos+1);
        }
        
        if(str.length()>m) answer = str;
        
        return answer;
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.nextLine();
        System.out.print(T.solution(str));
    }
}
```

## 배운점

- Scanner nextLine();

Scanner에서 공백을 포함한 한 줄을 받아들이고 싶으면 `{Scanner}.next();` 가 아닌 `{Scanner}.nextLine();`을 해주어야 한다.

- split();

String 객체에 `split();` 을 사용해서 원하는 단어를 기준으로 slice 하고 값을 배열로 받아볼 수 있다.

- indexOf();

String 객체에 `indexOf();` 를 사용해서 원하는 값의 index를 가져올 수 있다. 만약 해당 값이 없다면 **-1을 return 한다.**

- subString();

String 객체의 index와 subString을 사용해서 String 객체를 slice 할 수 있다.