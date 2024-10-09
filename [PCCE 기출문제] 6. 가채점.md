## 문제 설명
A반 학생들은 시험이 끝난 뒤 성적이 나오기 전 자기 시험지를 가채점해 보았습니다.<br>
이후에 선생님이 실제 성적을 불러 줄 때 가채점한 점수와 실제 성적이 다른 학생들이 있어<br>
선생님께 문의를 하려고 합니다.
<br><br>
성적을 문의하려는 학생들의 번호가 담긴 정수 리스트 numbers와<br>
가채점한 점수가 성적을 문의하려는 학생 순서대로 담긴 정수 리스트 our_score,<br>
실제 성적이 번호 순서대로 담긴 정수 리스트 score_list가 주어집니다.<br>
주어진 solution 함수는 가채점한 점수가 실제 성적과 동일하다면 "Same"을,<br>
다르다면 "Different"를 순서대로 리스트에 담아 return하는 함수입니다.<br>
solution 함수가 올바르게 작동하도록 한 줄을 수정해 주세요.<br>

## 출력 예시
numbers	    our_score	          score_list	                   result
[1]	          [100]	      [100, 80, 90, 84, 20]   	          ["Same"]
[3, 4]	     [85, 93]	[85, 92, 38, 93, 48, 85, 92, 56]	["Different", "Same"]

<br>
입출력 예 #1<br>
1번 학생이 가채점한 성적은 100점으로 <br>
실제 성적과 같기 때문에 "Same"을 담아 return합니다.<br>
<br>
입출력 예 #2<br>
3번 학생이 가채점한 성적은 85점으로<br>
실제 성적 38점과 다르기 때문에 "Different"를,<br>
4번 학생이 채점한 성적은 93점으로<br>
실제 성적과 같기 때문에 "Same"을 담아 return합니다.<br><br>
cpp를 응시하는 경우 리스트는 배열과 동일한 의미이니 풀이에 참고해주세요.
ex) 번호가 담긴 정수 리스트 numbers가 주어집니다.<br>
 => 번호가 담긴 정수 배열 numbers가 주어집니다.
<br><br>
java를 응시하는 경우 리스트는 배열, 함수는 메소드와 동일한 의미이니 풀이에 참고해주세요.
ex) solution 함수가 올바르게 작동하도록 한 줄을 수정해 주세요.<br>
 => solution 메소드가 올바르게 작동하도록 한 줄을 수정해 주세요.

 ## 내 문제 풀이
 ```
 class Solution {
    public String[] solution(int[] numbers, int[] our_score, int[] score_list) {
        int num_student = numbers.length;
        String[] answer = new String[num_student];

        for (int i = 0; i < num_student; i++) {
            if (our_score[i] == score_list[numbers[i]-1]) {
                answer[i] = "Same";
            }
            else {
                answer[i] = "Different";
            }
        }
```

