```java
//프로그래머스 요격 시스템
import java.util.*;
class Solution {
    public int solution(int[][] targets) {
        int answer = 0;
        
        if(targets.length==1)return 1;
        Arrays.sort(targets,(a,b)->a[1]-b[1]);
        int end=-1;
        for(int[] t: targets ){
            if(end==-1){
                answer++;
                end=t[1];
                continue;
            }
            if(t[0]<end)continue;
            answer++;
            end=t[1];
        }
        return answer;
    }
}
```