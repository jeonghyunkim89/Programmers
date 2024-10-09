## 문제 설명
여름이는 강아지를 산책시키려고 합니다.<br>
여름이는 2차원 좌표평면에서 동/서/남/북 방향으로 1m 단위로 이동하면서<br> 강아지를 산책시킵니다.<br>
산책루트가 담긴 문자열 route가 주어질 때,<br>
도착점의 위치를 return하도록 빈칸을 채워 solution함수를 완성해 주세요.<br><br>
route는 "N", "S", "E", "W"로 이루어져 있습니다.<br>
"N"은 북쪽으로 1만큼 움직입니다.<br>
"S"는 남쪽으로 1만큼 움직입니다.<br>
북쪽으로 -1만큼 움직인 것과 같습니다.<br>
"E"는 동쪽으로 1만큼 움직입니다.<br>
"W"는 서쪽으로 1만큼 움직입니다.<br>
동쪽으로 -1만큼 움직인 것과 같습니다.<br>
출발점으로부터 [동쪽으로 떨어진 거리, 북쪽으로 떨어진 거리]형태로<br>
강아지의 최종 위치를 구해서 return해야 합니다.<br>
출발점을 기준으로 서쪽, 남쪽에 있는 경우는<br>
동쪽, 북쪽으로 음수만큼 떨어진 것으로 표현합니다.<br>
출발점으로부터 동쪽으로 2, 북쪽으로 3만큼 떨어졌다면 [2, 3]을 return 합니다.<br>
출발점으로부터 서쪽으로 1, 남쪽으로 4만큼 떨어졌다면 [-1, -4]를 return 합니다.<br>

## 출력 예시
```
route	            result
"NSSNEWWN"	      [-1, 1]
"EESEEWNWSNWWNS"	[0, 0]
```

입출력 예 #1<br>
"NSSNEWWN" 순서대로 움직이면<br>
서쪽으로 1, 북쪽으로 1만큼 떨어진 곳에 도착하게 되므로<br>
[-1, 1]을 return합니다.<br>
<br>
입출력 예 #2<br>
"EESEEWNWSNWWNS" 순서대로 움직이면<br>
출발지와 같은 곳으로 돌아오므로 [0, 0]을 return합니다.<br>
<br>
cpp를 응시하는 경우 리스트는 배열과 동일한 의미이니 풀이에 참고해주세요.<br>
ex) 번호가 담긴 정수 리스트 numbers가 주어집니다.<br>
 => 번호가 담긴 정수 배열 numbers가 주어집니다.<br><br>

java를 응시하는 경우 리스트는 배열, 함수는 메소드와 동일한 의미이니<br> 풀이에 참고해주세요.<br>
ex) solution 함수가 올바르게 작동하도록 한 줄을 수정해 주세요.<br>
 => solution 메소드가 올바르게 작동하도록 한 줄을 수정해 주세요.<br><br>

## 내 문제 풀이
```
class Solution {
    public int[] solution(String route) {
        int east = 0;
        int north = 0;
        int[] answer = new int [2];
        for(int i=0; i<route.length(); i++){
            switch(route.charAt(i)){
                case 'N':
                    north++;
                    break;
                case 'S':
                    north--;
                    break;
                case 'E':
                    east++;
                    break;
                case 'W':
                    east--;
                    break;
            }
        }
        answer[0] = east;
        answer[1] = north;
        return answer;
    }
}
```
