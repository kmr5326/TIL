```java
//프로그래머스 경주로 건설
import java.util.*;
class Solution {
    static int n;
    static int[] dy={-1,1,0,0};
    static int[] dx={0,0,-1,1};

    public int solution(int[][] board) {
        int answer = 0;
        n=board.length;
        answer=bfs(board,0,0);
        return answer;
    }

    int bfs(int[][] board,int y,int x){
        Queue<Road> q=new ArrayDeque<>();
        int[][][] visit=new int[n][n][4];
        for(int[][] v1: visit){
            for(int[] v2:v1)Arrays.fill(v2,Integer.MAX_VALUE);
        }
        
        for(int i=0;i<4;i++){
            int ny= y + dy[i];
            int nx= x + dx[i];
            if(ny==-1 || nx==-1 || ny==n || nx==n)continue;
            if(board[ny][nx]==0){
                q.add(new Road(ny,nx,i,100));
                visit[ny][nx][i]=100;
            }
        }
        
        while(!q.isEmpty()){
            Road now=q.poll();
            if(now.y==n-1 && now.x==n-1){
                continue;
            }
            for(int i=0;i<4;i++){
                int ny=now.y+dy[i];
                int nx=now.x+dx[i];
                if(ny==-1 || nx==-1 || ny==n || nx==n)continue;
                int nextCost=now.cost+(now.d==i?100:600);
                if(board[ny][nx]==0){
                    if(visit[ny][nx][i]>nextCost){
                        q.add(new Road(ny,nx,i,nextCost));
                        visit[ny][nx][i]=nextCost;
                    }
                }
            }
        }
        int min=Integer.MAX_VALUE;
        for(int i=0;i<4;i++)min=Math.min(min,visit[n-1][n-1][i]);
        return min;
    }

    class Road{
        int y;
        int x;
        int d;
        int cost;

        public Road(int y,int x,int d,int c){
            this.y=y;
            this.x=x;
            this.d=d;
            cost=c;
        }

    }
}
```