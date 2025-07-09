```java
//프로그래머스 연속 펄스 부분 수열의 합
class Solution {
    public long solution(int[] sequence) {
        long answer = 0;
        
        long sum1=0;
        long sum2=0;
        long pulse=1;
        long sum1Min=0;
        long sum2Min=0;
        
        for(int s:sequence){
            sum1+=s*pulse;
            sum2+=s*-pulse;
            
            answer=Math.max(answer,Math.max(sum1-sum1Min,sum2-sum2Min));
            
            sum1Min=Math.min(sum1Min,sum1);
            sum2Min=Math.min(sum2Min,sum2);
            
            pulse*=-1;
        }
        return answer;
    }
}
```