```java
//프로그래머스 점 찍기
class Solution {
    public long solution(int k, int d) {
        long answer = 0;
        for(long x=0;x<=d;x+=k){
            long y=(long)Math.sqrt(Math.pow(d,2)-Math.pow(x,2));
            answer+=(long)(y/k)+1;
        }
        return answer;
    }
}
```