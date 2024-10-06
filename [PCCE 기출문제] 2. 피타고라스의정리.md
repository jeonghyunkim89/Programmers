## 문제 설명
직각삼각형이 주어졌을 때 빗변의 제곱은 다른 두 변을 각각 제곱한 것의 합과 같습니다.

<img src =
https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/45e3aa58-327f-4860-a634-2917ae76c159/%E1%84%91%E1%85%B5%E1%84%90%E1%85%A1%E1%84%80%E1%85%A9%E1%84%85%E1%85%A1%E1%84%89%E1%85%B3.jpg>

직각삼각형의 한 변의 길이를 나타내는 정수 a와 빗변의 길이를 나타내는 정수 c가 주어질 때, 다른 한 변의 길이의 제곱, b_square 을 출력하도록 한 줄을 수정해 코드를 완성해 주세요.

## 출력 예시
입력 #1
```
3
5
```

출력 #1
```
16   "a2 = 9, c2 = 25 이므로 16을 출력합니다."
```

입력 #2
```
9
10
```

출력 #2
```
19   "a2 = 81, c2 = 100 이므로 19를 출력합니다."
```

## 문제 풀이
```
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int c = sc.nextInt();

        int b_square = (int)Math.pow(c,2) - (int)Math.pow(a,2);

        System.out.println(b_square);
    }
}
```
