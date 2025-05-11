```java
//백준 순열의 순서
import java.io.*;
import java.util.*;
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine());
        int query = Integer.parseInt(st.nextToken());
        int[] used=new int[n+1];
        long[] fac=new long[21];
        fac[0]=1;
        for(int i=1;i<21;i++)fac[i]=fac[i-1]*i;

        if (query == 1) {
            long k=Long.parseLong(st.nextToken());
            ArrayList<Integer> ans=new ArrayList<>();
            for(int i=0;i<n;i++){
                for(int j=1;j<=n;j++){
                    if(used[j]==1)continue;
                    if(k>fac[n-i-1]){
                        k-=fac[n-i-1];
                    }
                    else{
                        used[j]=1;
                        ans.add(j);
                        break;
                    }
                }
            }
            for(int a:ans){
                System.out.print(a+" ");
            }
        } else {
            long ans=1;
            while(st.hasMoreTokens()){
                int num=Integer.parseInt(st.nextToken());
                int cnt=0;
                for(int i=1;i<num;i++){
                    if(used[i]==0){
                        cnt++;
                    }
                }
                ans+=cnt*fac[n-1];
                used[num]=1;
                n--;
            }
            System.out.println(ans);
        }

    }

}
```