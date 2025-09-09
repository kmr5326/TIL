```java
//프로그래머스 이모티콘 할인행사
import java.util.*;
class Solution {
    static int[] cost;
    static int[] answer;
    
    public int[] solution(int[][] users, int[] emoticons) {
        answer = new int[2];
        cost=new int[users.length];
        func(emoticons,users,0);
        return answer;
    }
    
    void func(int[] emoticons,int[][] users,int idx){
        if(idx==emoticons.length){
            int[] res=new int[2];
            for(int i=0;i<users.length;i++){
                if(cost[i]>=users[i][1])res[0]++;
                else res[1]+=cost[i];
            }
            if(res[0]>answer[0]){
                answer[0]=res[0];
                answer[1]=res[1];
            }
            else if(res[0]==answer[0]){
                if(res[1]>answer[1]){
                    answer[1]=res[1];
                }
            }
            return;
        }
        for(int i=1;i<=4;i++){
            int ratio=i*10;
            int price=emoticons[idx]*(100-ratio)/100;
            ArrayList<int[]> list=new ArrayList<>();
            for(int j=0;j<users.length;j++){
                if (cost[j] >= users[j][1]) continue;
                
                
                if(users[j][0]<=ratio){
                    cost[j]+=price;
                    list.add(new int[]{j,price});
                }
            }
            func(emoticons,users,idx+1);
            for(int[] a:list){
                cost[a[0]]-=a[1];
            }
        }
    }
}
```