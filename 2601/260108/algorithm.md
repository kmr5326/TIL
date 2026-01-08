```java
//프로그래머스 비밀 코드 해독
import java.util.*;
class Solution {
    ArrayList<ArrayList<Integer>> numList=new ArrayList<>();

    public int solution(int n, int[][] q, int[] ans) {
        int answer = 0;
        int[] nums=new int[n];

        for(int i=1;i<=n;i++){
            nums[i-1]=i;
        }

        makeSet(0,nums,new ArrayList<>());

        for(int i=0;i<numList.size();i++){
            ArrayList<Integer> set=numList.get(i);

            boolean result=true;
            for(int j=0;j<ans.length;j++){
                boolean ret=check(ans[j],set,q[j]);
                if(!ret)result=false;
                if(!result)break;
            }
            if(result){
                int aa=1;
                answer++;
            }
        }

        return answer;
    }

    public void makeSet(int idx,int[] nums,ArrayList<Integer> list){
        if(list.size()==5){
            ArrayList<Integer> copyList=new ArrayList<>();
            for(int a:list)copyList.add(a);
            numList.add(copyList);
            return;
        }

        for(int i=idx;i<nums.length;i++){
            list.add(nums[i]);
            makeSet(i+1,nums,list);
            list.remove(list.size()-1);
        }
    }

    public boolean check(int cnt,ArrayList<Integer> set,int[] nums){
        int count=0;
        for(int i=0;i<5;i++){
            if(set.contains(nums[i]))count++;
        }
        if(count==cnt)return true;
        else return false;
    }
}
```