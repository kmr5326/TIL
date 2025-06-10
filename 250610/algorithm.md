```java
//프로그래머스 홀짝트리
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Queue;

class Solution {
    static HashMap<Integer,ArrayList<Integer>> adj;
    static HashMap<Integer,Integer> treeTypeMap;
    public int[] solution(int[] nodes, int[][] edges) {
        int[] answer = {0,0};
        adj=new HashMap<>();
        for(int[] e:edges){
            int a=e[0];
            int b=e[1];
            adj.computeIfAbsent(a,k->new ArrayList<>()).add(b);
            adj.computeIfAbsent(b,k->new ArrayList<>()).add(a);
        }

        for(int node:nodes){
            treeTypeMap=new HashMap<>();
            dfs(node,new HashMap<>());
            int type=-1;
            int flag=0;
            for(int key:treeTypeMap.keySet()){
                if(type==-1){
                    type=treeTypeMap.get(key);
                    flag=type;
                    continue;
                }
                int treeType=treeTypeMap.get(key);
                if(type!=treeType){
                    flag=0;
                    break;
                }
            }
            if(flag==1)answer[0]++;
            else if(flag==2)answer[1]++;

        }
        return answer;
    }

    void dfs(int node,HashMap<Integer,Boolean> visit){
        visit.put(node,true);
        int cnt=0;
        ArrayList<Integer> arr=adj.getOrDefault(node,new ArrayList<>());
        for(int next:arr){
            if(!visit.getOrDefault(next,false)){
                dfs(next,visit);
                cnt++;
            }
        }
        if(node%2==0 && cnt%2==0)treeTypeMap.put(node,1);
        else if(node%2==1 && cnt%2==1)treeTypeMap.put(node,1);
        else treeTypeMap.put(node,2);
    }
}
```