```java
//프로그래머스 인사고과
import java.util.Arrays;

class Solution {
    public int solution(int[][] scores) {
        int answer = 0;

        int[] wanho=scores[0];

        Arrays.sort(scores,(a,b)->{
            if(a[0]==b[0])return a[1]-b[1];
            else return b[0]-a[0];
        });

        int rank=1;
        int wSum=wanho[0]+wanho[1];
        int max=0;
        for(int i=0;i<scores.length;i++){
            int sum=scores[i][0]+scores[i][1];
            if(max<=scores[i][1]){
                max=scores[i][1];
                if(sum>wSum)rank++;
            }
            else{
                if(scores[i].equals(wanho))return -1;
            }
            
        }
        answer=rank;
        return answer;
    }
}
```