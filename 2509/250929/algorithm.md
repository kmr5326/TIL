```java
//프로그래머스 둘만의 암호
class Solution {
    public String solution(String s, String skip, int index) {
        String answer = "";
        char[] charArr=s.toCharArray();

        for(int i=0;i<charArr.length;i++){
            int cnt=index;
            char c=charArr[i];
            while(cnt>0){
                c++;
                if(c>'z')c= (char) (c-26);
                if(skip.indexOf(c)==-1){
                    cnt--;
                }
            }
            charArr[i]=c;
        }
        answer=String.valueOf(charArr);
        return answer;
    }
}
```