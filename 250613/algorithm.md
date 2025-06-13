```java
//프로그래머스 최고의 집합
import java.util.*;
class Solution {
    public int[] solution(int n, int s) {
        int[] answer = {};
        if(s<n){
            answer=new int[]{-1};
            return answer;
        }
        
        int quotient=s/n;
        int rest=s%n;
        
        answer=new int[n];
        Arrays.fill(answer,quotient);
        if(rest!=0){
            for(int i=n-1;i>=0;i--){
                answer[i]+=1;
                rest-=1;
                if(rest==0)break;
            }
        }
        return answer;
    }
}
```