```java
//프로그래머스 거스름돈
import java.util.*;
class Solution {
    public int solution(int n, int[] money) {
        int answer = 0;
        int len=money.length;
        Arrays.sort(money);
        int[][] dp=new int[len+1][n+1];
        
        for(int i=1;i<len+1;i++){
            int m=money[i-1];
            dp[i][0]=1;
            for(int j=1;j<n+1;j++){
                dp[i][j]+=dp[i-1][j]%1000000007;
                if(j-m>=0)dp[i][j]+=dp[i][j-m]%1000000007;
            }
        }
        answer=dp[len][n];
        return answer;
    }
}
```