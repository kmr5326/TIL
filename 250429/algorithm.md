```java
//백준 사회망 서비스
import java.io.*;
import java.util.*;
public class Main {

    static int n;
    static int[] v;
    static ArrayList<Integer>[] edges;
    static int[][] dp;

    public static void main(String[] args) throws IOException{
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));

        n=Integer.parseInt(br.readLine());
        v=new int[n+1];
        edges=new ArrayList[n+1];
        for(int i=1;i<n+1;i++)edges[i]=new ArrayList<>();
        dp=new int[n+1][2];
        int start=1;
        for(int i=0;i<n-1;i++){
            StringTokenizer st=new StringTokenizer(br.readLine());
            int a=Integer.parseInt(st.nextToken());
            int b=Integer.parseInt(st.nextToken());
            edges[a].add(b);
            edges[b].add(a);
            start=a;
        }

        dfs(start);
        System.out.println(Math.min(dp[start][0],dp[start][1]));

    }

    static void dfs(int now){
        v[now]=1;
        dp[now][0]=1;
        for(int next:edges[now]){
            if(v[next]==0){
                dfs(next);
                dp[now][1]+=dp[next][0];
                dp[now][0]+=Math.min(dp[next][0],dp[next][1]);
            }

        }
    }

}
```