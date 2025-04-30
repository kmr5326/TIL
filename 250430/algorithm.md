```java
//백준 안전영역
import java.io.*;
import java.util.*;
public class Main {

    static int n;
    static int[][] map;
    static Set<Integer> set;
    static int[] dy={-1,1,0,0};
    static int[] dx={0,0,-1,1};

    public static void main(String[] args) throws IOException{
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        n=Integer.parseInt(br.readLine());

        map=new int[n][n];
        set=new HashSet<>();
        for(int i=0;i<n;i++){
            StringTokenizer st=new StringTokenizer(br.readLine());
            for(int j=0;j<n;j++){
                map[i][j]=Integer.parseInt(st.nextToken());
                set.add(map[i][j]);
            }
        }

        int ans=1;
        for(int a:set){
            int ret=raining(a,0);
            ans=Math.max(ans,ret);
        }
        System.out.println(ans);
    }

    static int raining(int a,int cnt){
        int[][] v=new int[n][n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                if(v[i][j]==0 && map[i][j]>a){
                    dfs(i,j,v,a);
                    cnt++;
                }
            }
        }
        return cnt;
    }

    static void dfs(int y,int x,int[][] v,int a){
        v[y][x]=1;
        for(int k=0;k<4;k++){
            int ny=y+dy[k];
            int nx=x+dx[k];
            if(ny==-1 || nx==-1 || ny==n || nx==n)continue;
            if(v[ny][nx]==0 && map[ny][nx]>a){
                dfs(ny,nx,v,a);
            }
        }
    }

}
```