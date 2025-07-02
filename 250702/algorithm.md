```java
//프로그래머스 다단계 칫솔 판매
import java.util.*;
class Solution {
    static HashMap<String,Integer> profit;
    static HashMap<String,String> parents;
    
    public int[] solution(String[] enroll, String[] referral, String[] seller, int[] amount) {
        int[] answer = {};
        profit=new HashMap<>();
        parents=new HashMap<>();
        for(int i=0;i<enroll.length;i++){
            profit.put(enroll[i],0);
            parents.put(enroll[i],referral[i]);
        }
        
        for(int i=0;i<seller.length;i++){
            calculate(seller[i],amount[i]*100);
        }
        
        answer=new int[enroll.length];
        for(int i=0;i<enroll.length;i++){
            answer[i]=profit.get(enroll[i]);
        }
        
        return answer;
    }
    
    void calculate(String name,int amount){
        String p=parents.get(name);
        int commission=(int)(amount*0.1);
        if(p.equals("-")){
            profit.put(name,profit.get(name)+amount-commission);
        }
        else{
            profit.put(name,profit.get(name)+amount-commission);
            if(commission>0)calculate(p,commission);
        }
    }
}
```