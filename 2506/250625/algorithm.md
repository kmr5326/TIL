```java
//프로그래머스 미로 탈출
import java.util.*;
class Solution {
    static int[] dy={-1,1,0,0};
    static int[] dx={0,0,-1,1};
    static char[][] map;
    static int n,m;
    
    public int solution(String[] maps) {
        int answer = Integer.MAX_VALUE;
        map=new char[maps.length][maps[0].length()];
        for(int i=0;i<maps.length;i++){
            map[i]=maps[i].toCharArray();
        }
        n=maps.length;
        m=maps[0].length();
        
        int sY=0;
        int sX=0;
        int lY=0;
        int lX=0;
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(maps[i].charAt(j)=='S'){
                    sY=i;
                    sX=j;
                }
                else if(maps[i].charAt(j)=='L'){
                    lY=i;
                    lX=j;
                }
            }
        }
        
        int ret1=bfs(sY,sX,'L');
        int ret2=bfs(lY,lX,'E');
        if(ret1==Integer.MAX_VALUE || ret2==Integer.MAX_VALUE)return -1;
        answer=ret1+ret2;
        
        return answer;
    }
    
    int bfs(int y,int x,char target){
        Queue<int[]> q=new ArrayDeque();
        int[][] visit=new int[n][m];
        visit[y][x]=1;
        q.add(new int[]{y,x,0});
        int ret=Integer.MAX_VALUE;
        while(!q.isEmpty()){
            int[] now=q.poll();
            for(int i=0;i<4;i++){
                int ny=now[0]+dy[i];
                int nx=now[1]+dx[i];
                if(ny==-1 || nx==-1 || ny==n || nx==m)continue;
                if(visit[ny][nx]==0){
                    if(map[ny][nx]!=target && map[ny][nx]!='X'){
                        q.add(new int[]{ny,nx,now[2]+1});
                        visit[ny][nx]=1;
                    }
                    else if(map[ny][nx]==target){
                        ret=Math.min(ret,now[2]+1);
                    }
                }
            }
        }
        return ret;
    }
}
```