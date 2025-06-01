```java
//백준 경로 찾기
import java.io.*;
import java.util.*;
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n=Integer.parseInt(br.readLine());
        int[][] adj=new int[n][n];
        for(int i=0;i<n;i++){
            StringTokenizer st=new StringTokenizer(br.readLine());
            for(int j=0;j<n;j++){
                adj[i][j]=Integer.parseInt(st.nextToken());
            }
        }

        int[][] dist=new int[n][n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                if(i==j)dist[i][j]=0;
                if(adj[i][j]>0)dist[i][j]=adj[i][j];
                else dist[i][j]=Integer.MAX_VALUE;
            }
        }

        for(int k=0;k<n;k++){
            for(int i=0;i<n;i++){
                for(int j=0;j<n;j++){
                    if(dist[i][k]==Integer.MAX_VALUE || dist[k][j]==Integer.MAX_VALUE)continue;
                    dist[i][j]=Math.min(dist[i][j],dist[i][k]+dist[k][j]);
                }
            }
        }

        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++) {
                if(dist[i][j]==Integer.MAX_VALUE) System.out.print(0+" ");
                else System.out.print(1+" ");
            }
            System.out.println();
        }
    }
}
```