```java
//프로그래머스 마법의 엘리베이터
import java.util.*;

class Solution {
    public int solution(int storey) {
        int answer = 0;
        while(storey>0){
            int remainder=storey%10;
            storey/=10;
            if(remainder>5){
                answer+=10-remainder;
                storey++;
            }
            else if(remainder==5){
                answer+=5;
                if(storey%10>=5){
                    storey++;
                }
            }
            else{
                answer+=remainder;
            }
            
        }
        return answer;
    }
}
```