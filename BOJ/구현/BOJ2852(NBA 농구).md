# 백준 2852번 NBA 농구
[백준 2852번](https://www.acmicpc.net/problem/2852)
```java
import java.io.*;
import java.util.*;

public class Main {

    static class Record{
        int team, time;
        Record(int team, int time){
            this.team = team;
            this.time = time;
        }
    }
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());

        int winTeam = 0, minute = 0, team1Score = 0, team2Score = 0, team1Time = 0, team2Time = 0;
        Record[] record = new Record[N];

        for(int i = 0; i < N; i++){
            StringTokenizer st = new StringTokenizer(br.readLine());
            int inputWinTeam = Integer.parseInt(st.nextToken());
            String tmp = st.nextToken();
            String[] split = tmp.split(":");
            // 분 단위로 기록하고 마지막에 시간으로 변환한다.
            minute = (Integer.parseInt(split[0]) * 60) + Integer.parseInt(split[1]);
            record[i] = new Record(inputWinTeam, minute);
        }

        // 첫 번째 기록은 비교용으로 따로 빼 놓는다.
        winTeam = record[0].team;
        if(winTeam == 1) team1Score++;
        else team2Score++;

        minute = record[0].time;

        for(int i = 1; i < N; i++){
            int tmpTeam = record[i].team;
            int tmpTime = record[i].time;

            if(team1Score > team2Score) team1Time += tmpTime - minute;
            else if(team1Score < team2Score) team2Time += tmpTime - minute;

            if(tmpTeam == 1) team1Score++;
            else team2Score++;

            // 이전 값을 빼주어야 하기 때문에 tmpTime을 넣는다.
            minute = tmpTime;
        }

        // 반복이 전부 끝나고 나서 맨 뒤에 있는 시간(마지막 득점한 시간)을 총 시간에서 뺀다.
        if(team1Score > team2Score){
            team1Time += (48 * 60 - minute);
        }
        if(team1Score < team2Score){
            team2Time += (48 * 60 - minute);
        }

        // 분을 시간으로 바꾸는 작업
        int h1 = team1Time / 60;
        int m1 = team1Time % 60;
        String hour1;
        String min1;

        if(h1 < 10) hour1 = "0" + Integer.toString(h1);
        else hour1 = Integer.toString(h1);

        if(m1 < 10) min1 = "0" + Integer.toString(m1);
        else min1 = Integer.toString(m1);

        int h2 = team2Time / 60;
        int m2 = team2Time % 60;
        String hour2;
        String min2;

        if(h2 < 10) hour2 = "0" + Integer.toString(h2);
        else hour2 = Integer.toString(h2);

        if(m2 < 10) min2 = "0" + Integer.toString(m2);
        else min2 = Integer.toString(m2);

        System.out.println(hour1+ ":" + min1);
        System.out.println(hour2+ ":" + min2);
    }
    
}
```