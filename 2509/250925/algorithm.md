```java
//프로그래머스 양과 늑대
class Solution {
    int[] visited;
    int res;
    
    public int solution(int[] info, int[][] edges) {
        int answer = 0;
        res=0;
        visited=new int[info.length];
        visited[0]=1;
        dfs(1,0,edges,info);
        answer=res;
        return answer;
    }
    
    void dfs(int sheep,int wolf,int[][] edges,int[] info){
        if(sheep>wolf){
            res=Math.max(res,sheep);
        }
        else return;
        
        for(int i=0;i<edges.length;i++){
            int p=edges[i][0];
            int c=edges[i][1];
            
            if(visited[p]==1 && visited[c]==0){
                visited[c]=1;
                if(info[c]==0){
                    dfs(sheep+1,wolf,edges,info);
                }
                else dfs(sheep,wolf+1,edges,info);
                visited[c]=0;
            }
        }
    }
}
```