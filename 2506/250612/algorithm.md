```java
//프로그래머스 숫자게임
import java.util.*;

class Solution {
    public int solution(int[] A, int[] B) {
        int answer = 0;
        Arrays.sort(A);
        Arrays.sort(B);
        int j=B.length-1;
        for(int i=A.length-1;i>=0;i--){
            if(A[i]<B[j]){
                answer++;
                j--;
            }
        }
        return answer;
    }

}
```