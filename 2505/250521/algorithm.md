```java
//백준 괄호의 값
import java.io.*;
import java.util.*;
public class Main {
    static Stack<Character> stack;

    public static void main(String[] args) throws IOException {
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        String s=br.readLine();
        stack=new Stack<>();
        int ans=0;
        int cal=1;
        for(int i=0;i<s.length();i++){
            char c=s.charAt(i);
            if(c=='('){
                stack.add(c);
                cal*=2;
            }
            else if(c=='['){
                stack.add(c);
                cal*=3;
            }
            else if(c==')'){
                if(stack.isEmpty()||stack.peek()=='['){
                    System.out.println(0);
                    return;
                }
                if(s.charAt(i-1)=='(')ans+=cal;
                stack.pop();
                cal/=2;
            }
            else if(c==']'){
                if(stack.isEmpty()||stack.peek()=='('){
                    System.out.println(0);
                    return;
                }
                if(s.charAt(i-1)=='[')ans+=cal;
                stack.pop();
                cal/=3;
            }
        }
        if(!stack.isEmpty()){
            System.out.println(0);
            return;
        }
        System.out.println(ans);
    }

}
```