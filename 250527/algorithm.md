```java
//백준 탑
import java.io.*;
import java.util.*;
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n=Integer.parseInt(br.readLine());
        Stack<int[]> stack=new Stack<>();
        StringTokenizer st=new StringTokenizer(br.readLine());
        for(int i=1;i<=n;i++){
            int now=Integer.parseInt(st.nextToken());
            while(!stack.isEmpty()){
                if(stack.peek()[0]>now){
                    System.out.print(stack.peek()[1]+" ");
                    break;
                }
                stack.pop();
            }
            if(stack.isEmpty()) System.out.print(0+" ");
            stack.add(new int[]{now,i});
        }

    }

}
```