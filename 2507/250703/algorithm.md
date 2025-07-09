```java
//프로그래머스 무인도 여행
import java.util.*;
class Solution {
    static int[][] visit;
    static int[] dy={-1,1,0,0};
    static int[] dx={0,0,-1,1};
    static ArrayList<Integer> list;
    static int n,m;
    
    public int[] solution(String[] maps) {
        int[] answer = {};
        visit=new int[maps.length][maps[0].length()];
        n=maps.length;
        m=maps[0].length();
        list=new ArrayList<>();
        
        for(int i=0;i<maps.length;i++){
            char[] arr=maps[i].toCharArray();
            for(int j=0;j<maps[i].length();j++){
                if(arr[j]!='X' && visit[i][j]==0){
                    bfs(i,j,maps);
                }
            }
        }
        Collections.sort(list);
        answer=new int[list.size()];
        for(int i=0;i<list.size();i++){
            answer[i]=list.get(i);
        }
        if(list.isEmpty())answer=new int[]{-1};
        return answer;
    }
    
    void bfs(int y,int x,String[] maps){
        visit[y][x]=1;
        Queue<int[]> q=new ArrayDeque<>();
        q.add(new int[]{y,x});
        int sum=maps[y].charAt(x)-'0';
        while(!q.isEmpty()){
            int[] now=q.poll();
            for(int i=0;i<4;i++){
                int ny=now[0]+dy[i];
                int nx=now[1]+dx[i];
                if(ny == -1 || nx==-1 || ny==n || nx==m || visit[ny][nx]==1)continue;
                char c=maps[ny].charAt(nx);
                if(c!='X'){
                    visit[ny][nx]=1;
                    q.add(new int[]{ny,nx});
                    sum+=c-'0';
                }
                
            }
        }
        list.add(sum);
    }
}
```