```java
//프로그래머스 빛의 경로 사이클
import java.util.*;
class Solution {
    static int n,m;
    static int[] dy={-1,0,1,0};
    static int[] dx={0,-1,0,1};
    static ArrayList<Integer> ans;
    static int[][][] visit;
    
    public int[] solution(String[] grid) {
        int[] answer = {};
        n=grid.length;
        m=grid[0].length();
        ans=new ArrayList<>();
        visit=new int[n][m][4];
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                for(int d=0;d<4;d++){
                    if(visit[i][j][d]==1)continue;
                    ans.add(checkCycle(i,j,d,grid));
                }
            }
        }
        answer=new int[ans.size()];
        for(int i=0;i<ans.size();i++)answer[i]=ans.get(i);
        Arrays.sort(answer);
        return answer;
    }
    
    int checkCycle(int y,int x,int dir,String[] grid){
        int cnt=0;
        while(visit[y][x][dir]==0){
            visit[y][x][dir]=1;
            cnt++;
            
            if(grid[y].charAt(x)=='L')dir=(dir+3)%4;
            if(grid[y].charAt(x)=='R')dir=(dir+1)%4;
            y=(y+dy[dir]+n)%n;
            x=(x+dx[dir]+m)%m;
        }
        return cnt;
        
    }
}
```