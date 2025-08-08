```java
//백준 스타트와 링크
import java.io.*;
import java.util.*;
public class Main {
    static int n;
    static int[][] arr;
    static int min,total;
    static int[] visited;

    public static void main(String[] args) throws IOException {
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        n=Integer.parseInt(br.readLine());
        arr=new int[n][n];
        min=Integer.MAX_VALUE;
        total=0;
        visited=new int[n];

        for(int i=0;i<n;i++){
            StringTokenizer st=new StringTokenizer(br.readLine());
            for(int j=0;j<n;j++){
                arr[i][j]=Integer.parseInt(st.nextToken());
                total+=arr[i][j];
            }
        }

        comb(0,0,0,new ArrayList<>());
        System.out.println(min);
    }

    static void comb(int cnt,int idx,int sum,ArrayList<Integer> list){
        if(cnt==n/2){
            ArrayList<Integer> linkTeam=new ArrayList<>();
            int linkSum=0;
            for(int i=0;i<n;i++){
                if(!list.contains(i)){
                    for(int a:linkTeam){
                        linkSum+=arr[a][i];
                        linkSum+=arr[i][a];
                    }
                    linkTeam.add(i);
                }
            }
            int gap=Math.abs(linkSum-sum);
            min=Math.min(min,gap);
            return;
        }

        for(int i=idx;i<n;i++){
            if(visited[i]==0){
                visited[i]=1;
                int newSum=sum;
                for(int a:list){
                    newSum+=arr[a][i];
                    newSum+=arr[i][a];
                }
                list.add(i);
                comb(cnt+1,i,newSum,list);
                list.remove(list.size()-1);
                visited[i]=0;
            }
        }
    }
}
```