```java
//프로그래머스 야근 지수
import java.util.*;

class Solution {
    public long solution(int n, int[] works) {
        long answer = 0;
        PriorityQueue<Integer> pq=new PriorityQueue<>(Collections.reverseOrder());
        for(int work:works){
            pq.add(work);
        }
        while(!pq.isEmpty() && n>0){
            int top=pq.poll();
            int target=-1;
            if(!pq.isEmpty())target=pq.peek()-1;
            if(target==-1){
                if(top>=n){
                    pq.add(top-n);
                    n=0;
                }
                break;
            }
            else{
                int gap=top-target;
                if(gap>=n){
                    pq.add(top-n);
                    n=0;
                    break;
                }
                else{
                    pq.add(top-gap);
                    n=n-gap;
                }
            }
        }
        while(!pq.isEmpty()){
            int top=pq.poll();
            answer+= (long) top *top;
        }
        return answer;
    }

}
```