```java
//프로그래머스 [1차]셔틀버스
import java.util.*;
class Solution {
    static PriorityQueue<String> pq;
    static String busTime,answer;
    static int originN;
    
    public String solution(int n, int t, int m, String[] timetable) {
        answer = "";
        pq=new PriorityQueue<>();
        for(String s:timetable)pq.add(s);
        originN=n;
        while(n>0){
            if(n==originN){
                busTime="09:00";
                n--;
                if(n==0)bus(busTime,m,true);
                else bus(busTime,m,false);
            }
            else{
                String[] split=busTime.split(":");
                int hour=Integer.parseInt(split[0]);
                int min=Integer.parseInt(split[1]);
                min+=t;
                if(min>=60){
                    hour++;
                    min=min%60;
                }
                busTime=String.format("%02d:%02d",hour,min);
                n--;
                if(n==0)bus(busTime,m,true);
                else bus(busTime,m,false);
            }
        }
        return answer;
    }
    
    void bus(String time,int m,boolean lastBus){
        if(!lastBus){
            for(int i=0;i<m;i++){
                if(pq.isEmpty())break;
                if(pq.peek().compareTo(time)<=0){
                    pq.poll();
                }
                else return;
            }
        }
        else{
            if(pq.size()<m){
                answer=time;
                return;
            }
            String last="";
            for(int i=0;i<m;i++){
                if(pq.peek().compareTo(time)>0){
                    answer=time;
                    return;
                }
                last=pq.poll();
            }
            String[] split=last.split(":");
            int hour=Integer.parseInt(split[0]);
            int min=Integer.parseInt(split[1]);
            if(min==0){
                min=59;
                hour--;
            }
            else min--;
            answer=String.format("%02d:%02d", hour, min);
            return;
        }
    }
}
```