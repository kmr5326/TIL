```java
//백준 케빈 베이컨의 6단계 법칙
import java.io.*;
import java.util.*;
public class Main {
    static int n,m;
    static int[][] adj;
    static int[][] dist;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st=new StringTokenizer(br.readLine());
        n=Integer.parseInt(st.nextToken());
        m=Integer.parseInt(st.nextToken());
        adj=new int[n+1][n+1];

        for(int i=0;i<m;i++){
            st=new StringTokenizer(br.readLine());
            int a=Integer.parseInt(st.nextToken());
            int b=Integer.parseInt(st.nextToken());
            adj[a][b]=1;
            adj[b][a]=1;
        }

        dist=new int[n+1][n+1];
        for(int i=0;i<n+1;i++){
            for(int j=0;j<n+1;j++){
                if(adj[i][j]==1)dist[i][j]=1;
                else dist[i][j]=Integer.MAX_VALUE;
            }
        }

        for(int k=1;k<n+1;k++){
            for(int i=1;i<n+1;i++){
                for(int j=1;j<n+1;j++){
                    if(dist[i][k]==Integer.MAX_VALUE || dist[k][j]==Integer.MAX_VALUE)continue;
                    dist[i][j]=Math.min(dist[i][j],dist[i][k]+dist[k][j]);
                }
            }
        }

        int minDist=Integer.MAX_VALUE;
        int minNum=n+1;
        for(int i=1;i<n+1;i++){
            int sum=0;
            for(int j=1;j<n+1;j++){
                sum+=dist[i][j];
            }
            if(sum<minDist){
                minDist=sum;
                minNum=i;
            }
            else if(sum==minDist){
                if(i<minNum){
                    minNum=i;
                }
            }
        }
        System.out.println(minNum);
    }
}
```