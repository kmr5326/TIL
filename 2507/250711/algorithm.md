```java
//프로그래머스 디펜스 게임
import java.util.*;

class Solution {
    public int solution(int n, int k, int[] enemy) {
        int answer = 0;
        
        if(k>=enemy.length){
            return enemy.length;
        }
        
        PriorityQueue<Integer> pq=new PriorityQueue<>();
        for(int i=0;i<enemy.length;i++){
            pq.add(enemy[i]);
            if(pq.size()>k){
                int e=pq.poll();
                if(e>n)return i;
                n-=e;
            }
            answer++;
        }
        
        return answer;
    }
}
```