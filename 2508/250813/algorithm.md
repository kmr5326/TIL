```java
//프로그래머스 홀짝트리
import java.util.*;
class Solution {
    static int[] degree;
    static int[] parents;
    
    public int[] solution(int[] nodes, int[][] edges) {
        int[] answer = {0,0};
        
        parents=new int[1000001];
        degree=new int[1000001];
        for(int i=1;i<1000001;i++)parents[i]=i;
        for(int i=0;i<edges.length;i++){
            int a=edges[i][0];
            int b=edges[i][1];
            degree[a]++;
            degree[b]++;
            union(a,b);
        }
        
        HashMap<Integer,TreeInfo> map=new HashMap<>();
        for(int node : nodes) {
            int group = find(node);
            
            TreeInfo t = map.getOrDefault(group, new TreeInfo());
            
            if((node % 2 == 0) && (degree[node] % 2 == 0)) {
                t.evenNode++;
            } else if((node % 2 == 1) && (degree[node] % 2 == 1)) {
                t.oddNode++;
            } else if((node % 2 == 0) && (degree[node] % 2 == 1)) {
                t.rEvenNode++;
            } else if((node % 2 == 1) && (degree[node] % 2 == 0)) {
                t.rOddNode++;
            }
            
            map.put(group, t);
        }
        
        for(int k:map.keySet()){
            TreeInfo t=map.get(k);
            if(t.isNormalTree())answer[0]++;
            if(t.isReverseTree())answer[1]++;
        }
        
        return answer;
    }
    
    int find(int x){
        if(x!=parents[x])parents[x]=find(parents[x]);
        return parents[x];
    }
    
    void union(int a,int b){
        if(a>b){
            int tmp=a;
            a=b;
            b=tmp;
        }
        
        a=find(a);
        b=find(b);
        
        if(a!=b){
            parents[b]=a;
        }
    }
    
    class TreeInfo{
        int evenNode;
        int oddNode;
        int rEvenNode;
        int rOddNode;
        
        public TreeInfo(){
            evenNode=0;
            oddNode=0;
            rEvenNode=0;
            rOddNode=0;
        }
        
        boolean isNormalTree(){
            if((evenNode==1 && oddNode==0) || (evenNode==0 && oddNode==1))return true;
            return false;
        }
        
        boolean isReverseTree(){
            if((rEvenNode==1 && rOddNode==0) || (rEvenNode==0 && rOddNode==1))return true;
            return false;
        }
    }
}
```