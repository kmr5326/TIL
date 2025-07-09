```java
//백준 문자열 게임2
import java.io.*;
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t=Integer.parseInt(br.readLine());

        while(t-->0){
            String s=br.readLine();
            int k=Integer.parseInt(br.readLine());
            int a=100001;
            int b=-1;
            int[] dat=new int[26];

            if(k==1){
                System.out.println("1 1");
                continue;
            }

            for(int i=0;i<s.length();i++) {
                dat[s.charAt(i)-'a']++;
            }

            for(int i=0;i<s.length();i++) {
                if (dat[s.charAt(i) - 'a'] < k) continue;

                int cnt = 1;
                for (int j = i + 1; j < s.length(); j++) {
                    if(s.charAt(i)==s.charAt(j))cnt++;

                    if(cnt==k){
                        a=Math.min(a,j-i+1);
                        b=Math.max(b,j-i+1);
                        break;
                    }
                }
            }

            if(a==100001 || b==-1) System.out.println(-1);
            else System.out.println(a+" "+b);
            }
        }
    }
```