# 프로그래머스 JadenCase 문자열 만들기
[프로그래머스 JadenCase 문자열 만들기](https://school.programmers.co.kr/learn/courses/30/lessons/12951)
```java
class Solution {
    public String solution(String s) {
        String answer = "";
        String[] arr = s.split(" ");
        for(int i = 0; i < arr.length; i++){
            String str = arr[i];
            if(str.length() == 0){ //공백을 잘라낸 후에도 공백이 있다면 그 공백은 살려서 answer에 저장
                answer += " "; // 문제에서 여러 개의 공백이 올 수 있다고 함
                
            }else{
                answer += str.substring(0, 1).toUpperCase(); //첫 단어 대문자
                answer += str.substring(1, str.length()).toLowerCase(); //나머지 소문자
                answer += " "; //단어를 변형하고 마지막에 공백 추가
            }
        }
        if(s.substring(s.length()-1, s.length()).equals(" ")){ // s 문자열의 맨 뒤에 공백이 있을 경우
            return answer; // else문에서 마지막에 공백을 추가했어서 바로 return을 하면 마지막에 공백이 살아있음
        }
        return answer.substring(0, answer.length() -1);// s 문자열의 맨 뒤에 빈 문자열이 없을 경우 공백 제거 
    }
}
```
* 문제에서의 split은 문자 사이에 있는 공백을 단위로 문자를 쪼개준다.
* s의 맨 마지막에 공백이 올 경우는 문자 사이가 아니기 때문에 공백이 몇 개가 와도 무시된다.
* 반면 맨 앞에 공백이 있고 뒤에 문자가 있다면 앞에 공백은 빈 문자열로 인식한다.