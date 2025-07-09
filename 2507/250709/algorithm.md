```java
//프로그래머스 리코쳇 로봇
import java.util.ArrayDeque;
import java.util.Queue;

class Solution {
    static int[] dy={-1,1,0,0};
    static int[] dx={0,0,-1,1};
    static int n,m;

    public int solution(String[] board) {
        int answer = 0;
        n=board.length;
        m=board[0].length();

        int sy=0;
        int sx=0;
        for(int i=0;i<n;i++){
            int j=board[i].indexOf("R");
            if(j!=-1){
                sy=i;
                sx=j;
                break;
            }
        }

        char[][] b=new char[n][m];
        for(int i=0;i<n;i++)b[i]=board[i].toCharArray();
        Queue<int[]> q=new ArrayDeque<>();
        q.add(new int[]{sy,sx});
        int[][] visit=new int[n][m];
        visit[sy][sx]=1;
        answer=-1;
        while(!q.isEmpty()){
            int[] now=q.poll();
            if(b[now[0]][now[1]]=='G'){
                answer=visit[now[0]][now[1]]-1;
                break;
            }

            for(int i=0;i<4;i++){
                int ny=now[0]+dy[i];
                int nx=now[1]+dx[i];
                while(true){
                    if(isInRange(ny,nx) && b[ny][nx]!='D'){
                        ny+=dy[i];
                        nx+=dx[i];
                    }
                    else{
                        ny-=dy[i];
                        nx-=dx[i];
                        break;
                    }
                }

                if(visit[ny][nx]==0){
                    q.add(new int[]{ny,nx});
                    visit[ny][nx]=visit[now[0]][now[1]]+1;
                }
            }
        }

        return answer;
    }

    public boolean isInRange(int x, int y){
        if(0 <= x && x < n && 0 <= y && y < m)
            return true;
        return false;
    }
}
```