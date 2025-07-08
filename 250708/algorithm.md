```java
//프로그래머스 숫자 카드 나누기
import java.util.*;
class Solution {
    public int solution(int[] arrayA, int[] arrayB) {
        int answer = 0;
        
        int gcdA=arrayA[0];
        int gcdB=arrayB[0];
        for(int i=1;i<arrayA.length;i++){
            gcdA=gcd(gcdA,arrayA[i]);
            gcdB=gcd(gcdB,arrayB[i]);
        }
        
        boolean check=true;
        for(int i=0;i<arrayB.length;i++){
            if(arrayB[i]%gcdA==0){
                check=false;
                break;
            }
        }
        if(check)answer=gcdA;
        
        check=true;
        for(int i=0;i<arrayA.length;i++){
            if(arrayA[i]%gcdB==0){
                check=false;
                break;
            }
        }
        if(check)answer=Math.max(answer,gcdB);
        
        return answer;
    }
    
    int gcd(int a,int b){
        while(b!=0){
            int tmp=a;
            a=b;
            b=tmp%b;
        }
        return a;
    }
}
```