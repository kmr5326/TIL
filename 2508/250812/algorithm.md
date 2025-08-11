```java
//프로그래머스 지게차와 크레인
import java.util.*;
class Solution {
    static int n,m;
    static char[][] arr;
    static int cnt;
    static int[] dy={-1,1,0,0};
    static int[] dx={0,0,-1,1};
    
    public int solution(String[] storage, String[] requests) {
        int answer = 0;
        
        n=storage.length;
        m=storage[0].length();
        arr=new char[n][m];
        cnt=n*m;
        for(int i=0;i<n;i++)arr[i]=storage[i].toCharArray();
        
        for(String r:requests){
            char c=r.charAt(0);
            if(r.length()==1){
                jeegae(c);
            }
            else{
                crane(c);
            }
        }
        answer=cnt;
        return answer;
    }
    
    void jeegae(char c){
        ArrayList<int[]> list=new ArrayList<>();
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(arr[i][j]==c){
                    boolean ret=check(i,j);
                    if(ret){
                        cnt--;
                        list.add(new int[]{i,j});
                    }
                }
            }
        }
        for(int[] l:list){
            arr[l[0]][l[1]]='0';
        }
    }
    
    void crane(char c){
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(arr[i][j]==c){
                    arr[i][j]='0';
                    cnt--;
                }
            }
        }
    }
    
    boolean check(int y,int x){
        Queue<int[]> q=new ArrayDeque<>();
        int[][] visit=new int[n][m];
        visit[y][x]=1;
        q.add(new int[]{y,x});
        while(!q.isEmpty()){
            int[] now=q.poll();
            for(int i=0;i<4;i++){
                int ny=now[0]+dy[i];
                int nx=now[1]+dx[i];
                if(ny==-1 || nx==-1 || ny==n || nx==m)return true;
                if(visit[ny][nx]==0 && arr[ny][nx]=='0'){
                    q.add(new int[]{ny,nx});
                    visit[ny][nx]=1;
                }
            }
        }
        
        return false;
    }
}
```