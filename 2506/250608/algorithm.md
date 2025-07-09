```java
// 프로그래머스 [PCCP 기출문제] 2번 / 석유 시추
import java.util.ArrayDeque;
import java.util.HashMap;
import java.util.Queue;

class Solution {
    static int n,m;
    static int[][] v;
    static int[] dy={-1,1,0,0};
    static int[] dx={0,0,-1,1};
    static HashMap<Integer,Integer> sizeMap;
    public int solution(int[][] land) {
        int answer = 0;
        n=land.length;
        m=land[0].length;

        v=new int[n][m];
        sizeMap=new HashMap<>();
        int key=2;
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(land[i][j]==1 && v[i][j]==0){
                    bfs(i,j,land,key);
                    key++;
                }
            }
        }
        int keyCnt=sizeMap.keySet().size();
        for(int i=0;i<m;i++){
            int[] check=new int[keyCnt+2];
            int sum=0;
            for(int j=0;j<n;j++){
                int keyIdx=land[j][i];
                if(keyIdx>=2 && check[keyIdx]==0){
                    sum+=sizeMap.get(keyIdx);
                    check[keyIdx]=1;
                }
            }
            answer=Math.max(answer,sum);
        }
        return answer;
    }

    void bfs(int y,int x,int[][] land,int key){
        Queue<int[]> q=new ArrayDeque<>();
        v[y][x]=1;
        int cnt=1;
        q.add(new int[]{y,x});
        while(!q.isEmpty()){
            int[] now=q.poll();
            land[now[0]][now[1]]=key;
            for(int i=0;i<4;i++){
                int ny=now[0]+dy[i];
                int nx=now[1]+dx[i];
                if(ny==-1 || nx==-1 || ny==n || nx==m)continue;
                if(land[ny][nx]==1 && v[ny][nx]==0){
                    q.add(new int[]{ny,nx});
                    cnt++;
                    v[ny][nx]=1;
                }
            }
        }
        sizeMap.put(key,cnt);
    }
}
```