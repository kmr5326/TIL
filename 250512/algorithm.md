```java
//백준 귀찮은 해강이
import java.io.*;
import java.util.*;

public class Main {
    static int[] parents;

    public static void main(String[] args) throws IOException{
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st=new StringTokenizer(br.readLine());
        int n=Integer.parseInt(st.nextToken());
        int m=Integer.parseInt(st.nextToken());

        parents=new int[n+1];
        for(int i=1;i<n+1;i++)parents[i]=i;

        for(int i=0;i<m;i++){
            st=new StringTokenizer(br.readLine());
            int a=Integer.parseInt(st.nextToken());
            int b=Integer.parseInt(st.nextToken());
            union(a,b);
        }

        st=new StringTokenizer(br.readLine());
        int cnt=0;
        int now=Integer.parseInt(st.nextToken());
        for(int i=1;i<n;i++){
            int next=Integer.parseInt(st.nextToken());
            if(find(now)!=find(next))cnt++;
            now=next;
        }
        System.out.println(cnt);
    }

    static int find(int x){
        if(x!=parents[x])parents[x]=find(parents[x]);
        return parents[x];
    }

    static void union(int a,int b){
        a= find(a);
        b= find(b);
        if(a==b)return;

        if(a>b){
            int tmp=a;
            a=b;
            b=tmp;
        }

        parents[b]=a;

    }
}
```