```java
//프로그래머스 징검다리 건너기
class Solution {
    public int solution(int[] stones, int k) {
        int answer = 0;
        int start=1;
        int end=0;
        for(int i=0;i<stones.length;i++){
            end=Math.max(end,stones[i]);
        }
        
        while(start<=end){
            int mid=(start+end)/2;
            int cnt=0;
            for(int i=0;i<stones.length;i++){
                if(stones[i]-mid<=0)cnt++;
                else cnt=0;
                if(cnt>=k)break;
            }
            
            if(cnt>=k){
                end=mid-1;
            }
            else{
                start=mid+1;
                answer=mid+1;
            }
        }
        return answer;
    }
}
```