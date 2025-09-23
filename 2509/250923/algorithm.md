```java
//프로그래머스 자물쇠와 열쇠
import java.util.*;
class Solution {
    public boolean solution(int[][] key, int[][] lock) {
        boolean answer = false;
        int n=lock.length;
        int m=key.length;
        int[][] newLock=new int[n+2*(m-1)][n+2*(m-1)];
        for(int i=0;i<newLock.length;i++)Arrays.fill(newLock[i],-1);
        int cnt=0;
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                newLock[i+(m-1)][j+(m-1)]=lock[i][j];
                if(lock[i][j]==0)cnt++;
            }
        }
        for(int t=0;t<4;t++){
            for(int i=0;i<newLock.length-(m-1);i++){
                for(int j=0;j<newLock.length-(m-1);j++){
                    boolean ret=check(i,j,key,newLock,cnt);
                    if(ret){
                        answer=true;
                        break;
                    }
                }
            }
            if(t!=3)key=rotate(key);
        }
        return answer;
    }
    
    int[][] rotate(int[][] arr){
        int size=arr.length;
        int[][] tmp=new int[size][size];
        for(int i=0;i<size;i++){
            for(int j=0;j<size;j++){
                tmp[j][size-1-i]=arr[i][j];
            }
        }
        return tmp;
    }
    
    boolean check(int y,int x,int[][] key,int[][] lock,int cnt){
        boolean ret=false;
        int count=0;
        for(int i=0;i<key.length;i++){
            for(int j=0;j<key.length;j++){
                if(key[i][j]==1 && lock[y+i][x+j]==1)return false;
                if(key[i][j]==1 && lock[y+i][x+j]==0)count++;
                if(count==cnt){
                    ret=true;
                    break;
                }
            }
        }
        return ret;
    }
}
```