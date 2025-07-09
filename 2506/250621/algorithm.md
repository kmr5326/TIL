```java
//프로그래머스 보석 쇼핑
import java.util.HashMap;
import java.util.HashSet;

class Solution {
    public int[] solution(String[] gems) {
        int[] answer = {};

        HashSet<String> gemTypes=new HashSet<>();
        HashMap<String,Integer> map=new HashMap<>();
        for(String s: gems){
            gemTypes.add(s);
            map.put(s,0);
        }

        HashSet<String> set=new HashSet<>();

        int l=0;
        int r=0;
        set.add(gems[0]);
        map.put(gems[0],1);
        answer=new int[]{0,gems.length-1};
        int len=gems.length;
        while(l<=r){
            if(set.size()==gemTypes.size()){
                if(len>r-l+1){
                    answer=new int[]{l,r};
                    len=r-l+1;
                }
                map.put(gems[l],map.get(gems[l])-1);
                if(map.get(gems[l])==0)set.remove(gems[l]);
                l++;
            }
            else if(set.size()<gemTypes.size()){
                r++;
                if(r== gems.length)break;
                set.add(gems[r]);
                map.put(gems[r],map.get(gems[r])+1);
            }
        }
        answer[0]++;
        answer[1]++;
        return answer;
    }
}
```