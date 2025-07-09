```java
//백준 카드 구매하기
import java.io.*;
import java.util.*;
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n=Integer.parseInt(br.readLine());
        StringTokenizer st=new StringTokenizer(br.readLine());
        int[] p=new int[n+1];
        for(int i=1;i<n+1;i++){
            p[i]=Integer.parseInt(st.nextToken());
        }

        int[] dp=new int[n+1];
        dp[1]=p[1];
        for(int i=2;i<n+1;i++){
            for(int j=1;j<n+1;j++){
                if(i-j>=0){
                    dp[i]=Math.max(dp[i],dp[i-j]+p[j]);
                }
            }
        }
        System.out.println(dp[n]);
    }

}
```