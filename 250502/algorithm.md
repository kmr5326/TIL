```java
//백준 평범한배낭
import java.io.*;
import java.util.*;
public class Main {

    public static void main(String[] args) throws IOException{
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st=new StringTokenizer(br.readLine());
        int n=Integer.parseInt(st.nextToken());
        int k=Integer.parseInt(st.nextToken());
        int[][] items=new int[n+1][2];
        for(int i=1;i<n+1;i++){
            st=new StringTokenizer(br.readLine());
            items[i][0]=Integer.parseInt(st.nextToken());
            items[i][1]=Integer.parseInt(st.nextToken());
        }

        Arrays.sort(items,(x,y)->x[0]!=y[0]?x[0]-y[0]:x[1]-y[1]);

        int[][] dp=new int[n+1][k+1];
        int max=0;
        for(int i=1;i<n+1;i++){
            int w=items[i][0];
            int v=items[i][1];
            for(int j=0;j<k+1;j++){
                if(j-w>=0){
                    dp[i][j]=Math.max(dp[i-1][j],dp[i-1][j-w]+v);
                }
                else{
                    dp[i][j]=dp[i-1][j];
                }
                max=Math.max(max,dp[i][j]);
            }

        }
        System.out.println(max);
    }

}
```
```java
//백준 퇴사
import java.io.*;
import java.util.*;
public class Main {

    public static void main(String[] args) throws IOException{
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        int n=Integer.parseInt(br.readLine());
        int[][] meetings=new int[n+1][2];
        for(int i=1;i<n+1;i++){
            StringTokenizer st=new StringTokenizer(br.readLine());
            meetings[i][0]=Integer.parseInt(st.nextToken());
            meetings[i][1]=Integer.parseInt(st.nextToken());
        }

        int[] dp=new int[n+2];
        int max=0;
        for(int i=n;i>0;i--){
            int t=meetings[i][0];
            int p=meetings[i][1];
            if(i+t<=n+1){
                dp[i]=Math.max(dp[i+1],dp[i+t]+p);
            }
            else dp[i]=dp[i+1];
            max=Math.max(max,dp[i]);
        }
        System.out.println(max);
    }

}
```