```java
//백준 내려가기
import java.io.*;
import java.util.*;
public class Main {
    
    public static void main(String[] args) throws IOException{
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        int n=Integer.parseInt(br.readLine());
        int[][] nums=new int[n+1][3];
        int[][] maxDp=new int[n+1][3];
        int[][] minDp=new int[n+1][3];

        for(int i=1;i<n+1;i++){
            StringTokenizer st=new StringTokenizer(br.readLine());
            for(int j=0;j<3;j++){
                nums[i][j]=Integer.parseInt(st.nextToken());
            }
        }

        for(int i=0;i<3;i++){
            maxDp[1][i]=nums[1][i];
            minDp[1][i]=nums[1][i];
        }

        for(int i=2;i<n+1;i++){
            for(int j=0;j<3;j++){
                if(j==0){
                    maxDp[i][j]=Math.max(maxDp[i-1][j]+nums[i][j],maxDp[i-1][j+1]+nums[i][j]);
                    minDp[i][j]=Math.min(minDp[i-1][j]+nums[i][j],minDp[i-1][j+1]+nums[i][j]);
                }
                else if(j==1){
                    maxDp[i][j]=Math.max(maxDp[i-1][j-1]+nums[i][j],Math.max(maxDp[i-1][j]+nums[i][j],maxDp[i-1][j+1]+nums[i][j]));
                    minDp[i][j]=Math.min(minDp[i-1][j-1]+nums[i][j],Math.min(minDp[i-1][j]+nums[i][j],minDp[i-1][j+1]+nums[i][j]));
                }
                else if(j==2){
                    maxDp[i][j]=Math.max(maxDp[i-1][j]+nums[i][j],maxDp[i-1][j-1]+nums[i][j]);
                    minDp[i][j]=Math.min(minDp[i-1][j]+nums[i][j],minDp[i-1][j-1]+nums[i][j]);
                }
            }
        }

        int max=Integer.MIN_VALUE;
        int min=Integer.MAX_VALUE;
        for(int i=0;i<3;i++){
            max=Math.max(max,maxDp[n][i]);
            min=Math.min(min,minDp[n][i]);
        }
        System.out.println(max+" "+min);
    }

}
```

```java
//백준 회전초밥
import java.io.*;
import java.util.*;
public class Main {

    public static void main(String[] args) throws IOException{
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st=new StringTokenizer(br.readLine());
        int n=Integer.parseInt(st.nextToken());
        int d=Integer.parseInt(st.nextToken());
        int k=Integer.parseInt(st.nextToken());
        int c=Integer.parseInt(st.nextToken());
        int[] sushi=new int[n*2];
        for(int i=0;i<n;i++)sushi[i]=Integer.parseInt(br.readLine());
        for(int i=n;i<n*2;i++)sushi[i]=sushi[i%n];

        int ans=0;
        Map<Integer,Integer> map=new HashMap<>();
        for(int i=0;i<n+k;i++){
            if(i<=k-1){
                map.put(sushi[i],map.getOrDefault(sushi[i],0)+1);
                if(i==k-1){
                    if(map.containsKey(c))ans=Math.max(ans,map.keySet().size());
                    else ans=Math.max(ans,map.keySet().size()+1);
                }
            }
            else{
                map.put(sushi[i-k], map.get(sushi[i-k])-1);
                if(map.get(sushi[i-k])==0)map.remove(sushi[i-k]);
                map.put(sushi[i],map.getOrDefault(sushi[i],0)+1);
                if(map.containsKey(c))ans=Math.max(ans,map.keySet().size());
                else ans=Math.max(ans,map.keySet().size()+1);
            }
        }
        System.out.println(ans);
    }

}
```