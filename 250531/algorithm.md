```java
//백준 오큰수
import java.io.*;
import java.util.*;
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int n=Integer.parseInt(br.readLine());
        StringTokenizer st=new StringTokenizer(br.readLine());
        int[] nums=new int[n];
        for(int i=0;i<n;i++){
            nums[i]=Integer.parseInt(st.nextToken());
        }

        int[] ans=new int[n];
        Stack<Integer> stack=new Stack<>();
        for(int i=n-1;i>=0;i--){
            if(stack.isEmpty()){
                ans[i]=-1;
                stack.add(nums[i]);
            }
            else{
                boolean flag=false;
                while(!stack.isEmpty()){
                    if(stack.peek()>nums[i]){
                        ans[i]=stack.peek();
                        stack.add(nums[i]);
                        flag=true;
                        break;
                    }
                    else{
                        stack.pop();
                    }
                }
                if(stack.isEmpty() && !flag){
                    stack.add(nums[i]);
                    ans[i]=-1;
                }
            }
        }
        StringBuilder sb=new StringBuilder();
        for(int a:ans){
            sb.append(a);
            sb.append(" ");
        }
        System.out.println(sb);
    }

}
```