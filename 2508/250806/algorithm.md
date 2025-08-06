```java
//프로그래머스 풍선 터트리기
class Solution {
    public int solution(int[] a) {
        int n=a.length;
        int[] leftMin=new int[n];
        int[] rightMin=new int[n];
        int l=a[0];
        int r=a[n-1];
        
        for(int i=1;i<n;i++){
            if(l>a[i])l=a[i];
            leftMin[i]=l;
        }
        
        for(int i=n-2;i>=0;i--){
            if(r>a[i])r=a[i];
            rightMin[i]=r;
        }
        
        if(n==1)return 1;
        int answer = 2;
        for(int i=1;i<n-1;i++){
            if(a[i]>leftMin[i] && a[i]>rightMin[i])continue;
            answer++;
        }
        return answer;
    }
}
```