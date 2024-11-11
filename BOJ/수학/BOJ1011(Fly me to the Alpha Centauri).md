# 백준 1011번 Fly me to the Alpha Centauri
[백준 1011번](https://www.acmicpc.net/problem/1011)
```java
import java.util.*;
import java.io.*;

public class Main {
 
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int T = Integer.parseInt(br.readLine()); 
		
		for(int i = 0; i < T; i++) {
			
			StringTokenizer st = new StringTokenizer(br.readLine()," ");
			
			int X = Integer.parseInt(st.nextToken());
			int Y = Integer.parseInt(st.nextToken());
			
			int distance = Y - X;
			
			int max = (int)Math.sqrt(distance);
			
			if(max == Math.sqrt(distance)) {
                System.out.println(max * 2 - 1);
			}
			else if(distance <= max * max + max) {
                System.out.println(max * 2);
			}
			else {
                System.out.println(max * 2 + 1);
			}
			
		}
	}
 
}
```