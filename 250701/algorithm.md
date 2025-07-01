```java
//프로그래머스 하노이의탑
import java.util.ArrayList;

class Solution {
    static ArrayList<int[]> ansList;

    public int[][] solution(int n) {
        int[][] answer = {};
        ansList=new ArrayList<>();
        hanoi(n,1,3,2);
        answer=new int[ansList.size()][2];
        for(int i=0;i< ansList.size();i++){
            answer[i]=ansList.get(i);
        }
        return answer;
    }

    void hanoi(int n,int start,int target,int via){
        if(n==1){
            ansList.add(new int[]{start,target});
            return;
        }

        hanoi(n-1,start,via,target);
        hanoi(1,start,target,via);
        hanoi(n-1,via,target,start);
    }
}
```