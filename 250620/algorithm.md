```java
//프로그래머스 호텔 대실
import java.util.Arrays;
import java.util.PriorityQueue;

class Solution {
    public int solution(String[][] book_time) {
        int answer = 0;
        Arrays.sort(book_time,(x,y)->x[0].compareTo(y[0]));
        PriorityQueue<String[]> pq=new PriorityQueue<>((x,y)->x[1].compareTo(y[1]));
        for(String[] b:book_time){
            if(pq.isEmpty()){
                pq.add(b);
            }
            else{
                String[] finishTime=pq.peek()[1].split(":");
                String[] nowStartTime=b[0].split(":");
                int fT=Integer.parseInt(finishTime[0])*60+Integer.parseInt(finishTime[1]);
                int nST=Integer.parseInt(nowStartTime[0])*60+Integer.parseInt(nowStartTime[1]);
                if(nST-fT>=10){
                    pq.poll();
                    pq.add(b);
                }
                else pq.add(b);
            }
            answer=Math.max(answer,pq.size());
        }
        answer=Math.max(answer,pq.size());
        return answer;
    }
}
```