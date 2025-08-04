```java
//프로그래머스 퍼즐 게임 챌린지
class Solution {
    public int solution(int[] diffs, int[] times, long limit) {
        int answer = 0;
        
        int min=Integer.MAX_VALUE;
        int max=Integer.MIN_VALUE;
        for(int i=0;i<diffs.length;i++){
            max=Math.max(max,diffs[i]);
            min=Math.min(min,diffs[i]);
        }
        
        while(min<=max){
            int mid=(min+max)/2;
            long timeSum=0;
            
            boolean fail=false;
            for(int i=0;i<diffs.length;i++){
                int dif=diffs[i];
                if(dif<=mid){
                    timeSum+=times[i];
                }
                else{
                    int prev=0;
                    if(i!=0)prev=times[i-1];
                    timeSum+=(times[i]+prev)*(dif-mid)+times[i];
                }
                if(timeSum>limit){
                    fail=true;
                    break;
                }
            }

            if(fail){
                min=mid+1;
            }
            else{
                max=mid-1;
                answer=mid;
            }
        }
        return answer;
    }
}
```