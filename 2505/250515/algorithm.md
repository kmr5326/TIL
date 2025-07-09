```java
//프로그래머스 서버 증설 횟수
import java.util.*;
class Solution {
    static Queue<Server> q;
        public int solution(int[] players, int m, int k) {
            int answer = 0;
            q=new ArrayDeque<>();
            for(int i=0;i<24;i++){
                int p=players[i];
                checkQ(k,i);
                if(p<m)continue;
                if(p/m>q.size()){
                    int cnt=p/m-q.size();
                    answer+=cnt;
                    for(int j=0;j<cnt;j++){
                        q.add(new Server(i));
                    }
                }
            }
            return answer;
        }

        static void checkQ(int k,int nowTime){
            while(!q.isEmpty()){
                if(q.peek().startTime+k<=nowTime)q.poll();
                else break;
            }
        }

        static class Server{
            int startTime;

            public Server(int t){
                startTime=t;
            }
        }
}
```