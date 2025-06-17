```java
//프로그래머스 연속된 부분 수열의 합
class Solution {
    public int[] solution(int[] sequence, int k) {
        int[] answer = {0,0};
        int n=sequence.length;
        int l=n-1;
        int r=n-1;
        int sum=sequence[r];
        int size=1000005;
        while(l<=r){
            if(sum<k){
                l--;
                if(l==-1)break;
                sum+=sequence[l];
            }
            else if(sum>k){
                if(l==r && l==0)break;
                else if(l==r && l!=0){
                    l--;
                    sum+=sequence[l];
                }
                else {
                    sum -= sequence[r];
                    r--;
                }
            }
            else if(sum==k){
                if(size>=r-l+1){
                    size=r-l+1;
                    answer[0]=l;
                    answer[1]=r;
                }
                if(l==r && l==0){
                    break;
                }
                if(l==r && l!=0){
                    l--;
                    sum+=sequence[l];
                }
                else {
                    sum-=sequence[r];
                    r--;
                }
            }
        }
        return answer;
    }
}
```