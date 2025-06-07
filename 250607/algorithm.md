```java
//백준 내리막 길
import java.io.*;
import java.util.*;
public class Main {
    static int n,m;
    static int[][] board;
    static int[][] dp;
    static int ans;
    static int[] dy={-1,1,0,0};
    static int[] dx={0,0,-1,1};
    static int ty,tx;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st=new StringTokenizer(br.readLine());
        n=Integer.parseInt(st.nextToken());
        m=Integer.parseInt(st.nextToken());
        board=new int[n][m];
        for(int i=0;i<n;i++){
            st=new StringTokenizer(br.readLine());
            for(int j=0;j<m;j++){
                board[i][j]=Integer.parseInt(st.nextToken());
            }
        }

        dp=new int[n][m];
        for(int i=0;i<n;i++){
            Arrays.fill(dp[i],-1);
        }
        ty=n-1;
        tx=m-1;
        ans=dfs(0,0);
        System.out.println(ans);
    }

    static int dfs(int y,int x){
        if(y==ty && x==tx){
            return 1;
        }
        if(dp[y][x]!=-1)return dp[y][x];
        dp[y][x]=0;
        for(int i=0;i<4;i++){
            int ny=y+dy[i];
            int nx=x+dx[i];
            if(ny==-1 || nx==-1 || ny==n || nx==m)continue;
            if(board[ny][nx]>=board[y][x])continue;
            dp[y][x]=dp[y][x]+dfs(ny,nx);
        }
        return dp[y][x];
    }
}
```