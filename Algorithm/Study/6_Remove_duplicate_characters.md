# 중복 문자 제거

## 설명

소문자로 된 한개의 문자열이 입력되면 중복된 문자를 제거하고 출력하는 프로그램을 작성하세요.  
중복이 제거된 문자열의 각 문자는 원래 문자열의 순서를 유지합니다.

## 입력

첫 줄에 문자열이 입력됩니다. 문자열의 길이는 100을 넘지 않는다.

## 출력

첫 줄에 중복문자가 제거된 문자열을 출력합니다.

## 예시 입력 1

```
ksekkset

```

## 예시 출력 1

```
kset
```

## 나의 풀이(통과)

```java
import java.util.Scanner;

class Main {
    public String solution(String str){
        String answer = "";

        for(char c: str.toCharArray()){
            int count = answer.length() - answer.replace(Character.toString(c), "").length();
            if(count==0) answer+=c;
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

## 다른 풀이

```jsx
import java.util.Scanner;

class Main {
    public String solution(String str){
        String answer = "";
        for(int i=0; i<str.length(); i++){
            if(str.indexOf(str.charAt(i))==i) answer+=str.charAt(i);
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

## 배운점

- String의 ‘+’ 연산

String + char 도 가능하다.

- replace()

String 에는 replace 함수가 존재한다.

- indexOf()

가장 앞자리의 index를 return 한다.   
이 때 char형을 넣어야 하기 때문에 index에 들어가는 파라미터는 charAt으로 char형으로 변환시줘야한다.

- 중복을 계산하는 여러가지 방법
1. 처음 등장하는 문자가 결국 해당 인덱스와 일치한다면, 처음 등장하는 문자이며 이는 중복이 없음을 뜻한다.
2. 전체 문장에서 해당 문자를 replace 한 뒤 빼주었을 때 갯수가 1개라면 그것은 중복이 없음을 뜻한다.