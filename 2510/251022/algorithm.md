```java
//프로그래머스 110 옮기기
import java.util.*;
class Solution {
    public String[] solution(String[] s) {
        String[] answer = new String[s.length];
        
        for(int i=0;i<s.length;i++){
            String str=s[i];
            StringBuilder sb=new StringBuilder();
            StringBuilder insertSb=new StringBuilder();
            int cnt=0;
            for (int j = 0; j < str.length(); j++) {
                sb.append(str.charAt(j));
                int len = sb.length();
                if (len >= 3
                        && sb.charAt(len - 3) == '1'
                        && sb.charAt(len - 2) == '1'
                        && sb.charAt(len - 1) == '0') {
                    sb.setLength(len - 3);
                    cnt++;
                }
            }
            
            for(int j=0;j<cnt;j++)insertSb.append("110");
            int start=sb.lastIndexOf("0");
            start+=1;
            sb.insert(start,insertSb.toString());
            answer[i]=sb.toString();
        }
        return answer;
    }
}
```