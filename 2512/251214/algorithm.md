```java
//프로그래머스 스타 수열
class Solution {
    public int solution(int[] a) {
        int answer = 0;
        int[] cnt=new int[a.length];
        for(int i=0;i<a.length;i++){
            cnt[a[i]]++;
        }
        
        for(int i=0;i<cnt.length;i++){
            if(cnt[i]==0)continue;
            if(cnt[i]<answer)continue;
            
            int len=0;
            for(int j=0;j<a.length-1;j++){
                if(a[j]!=a[j+1] && (i==a[j] || i==a[j+1])){
                    len++;
                    j++;
                }
            }
            answer=Math.max(len,answer);
        }
        return answer*2;
    }
}
```