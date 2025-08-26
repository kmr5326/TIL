```java
class Solution {
    public int solution(int[][] board, int[][] skill) {
        int answer = 0;
        int n=board.length;
        int m=board[0].length;
        int[][] sum=new int[n+1][m+1];
        
        for(int[] s:skill){
            int val=s[5];
            if(s[0]==1)val*=-1;
            sum[s[1]][s[2]]+=val;
            sum[s[1]][s[4]+1]+=-1*val;
            sum[s[3]+1][s[2]]+=-1*val;
            sum[s[3]+1][s[4]+1]+=val;
        }
        
        for(int i=0;i<n+1;i++){
            for(int j=1;j<m+1;j++){
                sum[i][j]+=sum[i][j-1];
            }
        }
        
        for(int i=0;i<m+1;i++){
            for(int j=1;j<n+1;j++){
                sum[j][i]+=sum[j-1][i];
            }
        }
        
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(sum[i][j]+board[i][j]>0)answer++;
            }
        }
        return answer;
    }
}
```