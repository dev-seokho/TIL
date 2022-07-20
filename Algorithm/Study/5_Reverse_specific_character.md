# 특정 문자 뒤집기

## 설명

영어 알파벳과 특수문자로 구성된 문자열이 주어지면 영어 알파벳만 뒤집고,  
특수문자는 자기 자리에 그대로 있는 문자열을 만들어 출력하는 프로그램을 작성하세요.

## 입력

첫 줄에 길이가 100을 넘지 않는 문자열이 주어집니다.

## 출력

첫 줄에 알파벳만 뒤집힌 문자열을 출력합니다.

## 예시 입력 1

```
a#b!GE*T@S

```

## 예시 출력 1

```
S#T!EG*b@a
```

## 나의 풀이 (통과 못함)

```java
import java.util.Scanner;

class Main {
    public String solution(String str){

        char[] charArray = str.toCharArray();
        int lt = 0, rt = str.length()-1;

        while(lt < rt){
            if((charArray[lt] >= 'a' && charArray[lt] <= 'z') || (charArray[lt] >= 'A' && charArray[lt] <= 'Z')) {
                if ((charArray[rt] >= 'a' && charArray[rt] <= 'z') || (charArray[rt] >= 'A' && charArray[rt] <= 'Z')) {
                    char tmp = charArray[lt];
                    charArray[lt] = charArray[rt];
                    charArray[rt] = tmp;
                }
            }
            lt++;
            rt--;
        }

        return String.valueOf(charArray);
    }

    public static void main(String[] args){
        Main T = new Main();
        Scanner kb = new Scanner(System.in);
        String str = kb.next();

        System.out.println(T.solution(str));
    }
}
```

## 풀이

```java
import java.util.Scanner;

class Main {
    public String solution(String str){
        char[] s = str.toCharArray();
        int lt = 0, rt = str.length()-1;

        while(lt < rt){
            if(!Character.isAlphabetic(s[lt])) lt++;
            else if(!Character.isAlphabetic(s[rt])) rt--;
            else{
                char tmp = s[lt];
                s[lt] = s[rt];
                s[rt] = tmp;
                lt++;
                rt--;
            }
        }
        return String.valueOf(s);
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

- **문제파악**

충분히 풀 수 있는 문제였는데도 초기 문제파악이 잘 안됐다.
문제파악을 잘하도록 노력해봐야겠다.

- Character.isAlphabetic();

char 변수가 알파벳인지 확인하는 방법은 Character.isAlphabetic()을 활용하면 된다.