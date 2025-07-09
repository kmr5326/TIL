```java
//프로그래머스 줄 서는 방법
import java.util.*;
class Solution {
    public int[] solution(int n, long k) {
        int[] answer = new int[n];
        ArrayList<Integer> arr=new ArrayList<>();
        
        long f=1;
        for(int i=0;i<n;i++){
            arr.add(i+1);
            f*=(i+1);
        }
        
        k--;
        int idx=0;
        while(idx<n){
            f/=(n-idx);
            answer[idx++]=arr.remove((int)(k/f));
            k%=f;
        }

        return answer;
    }
}
```