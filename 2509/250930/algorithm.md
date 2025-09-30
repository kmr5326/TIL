```java
//프로그래머스 행렬 테두리 회전하기
class Solution {
    
    public int[] solution(int rows, int columns, int[][] queries) {
        int[] answer = new int[queries.length];
        int[][] arr=new int[rows][columns];
        int val=1;
        for(int i=0;i<rows;i++){
            for(int j=0;j<columns;j++){
                arr[i][j]=val++;
            }
        }
        
        int idx=0;
        for(int[] q:queries){
            answer[idx++]=rotate(arr,q[0]-1,q[1]-1,q[2]-1,q[3]-1);    
        }
        
        return answer;
    }
    
    int rotate(int[][] arr,int x1,int y1,int x2,int y2){
        int tmp=arr[x1][y1];
        int min=tmp;
        
        for(int i=x1;i<x2;i++){
            arr[i][y1]=arr[i+1][y1];
            min=Math.min(min,arr[i][y1]);
        }
        
        for(int i=y1;i<y2;i++){
            arr[x2][i]=arr[x2][i+1];
            min=Math.min(min,arr[x2][i]);
        }
        
        for(int i=x2;i>x1;i--){
            arr[i][y2]=arr[i-1][y2];
            min=Math.min(min,arr[i][y2]);
        }
        
        for(int i=y2;i>y1;i--){
            arr[x1][i]=arr[x1][i-1];
            min=Math.min(min,arr[x1][i]);
        }
        
        arr[x1][y1+1]=tmp;
        
        return min;
    }
}
```