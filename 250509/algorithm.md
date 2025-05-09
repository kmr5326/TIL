```java
//백준 미세먼지 안녕!
import java.io.*;
import java.util.*;
public class Main {
    static int r,c,t;
    static int[][] map;
    static int[][] robot;
    static int[][] spreadMap;
    static int[] dy={-1,1,0,0};
    static int[] dx={0,0,-1,1};

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st=new StringTokenizer(br.readLine());
        r=Integer.parseInt(st.nextToken());
        c=Integer.parseInt(st.nextToken());
        t=Integer.parseInt(st.nextToken());
        map=new int[r][c];
        robot=new int[2][2];
        int robotIdx=0;

        for(int i=0;i<r;i++){
            st=new StringTokenizer(br.readLine());
            for(int j=0;j<c;j++){
                int a=Integer.parseInt(st.nextToken());
                map[i][j]=a;
                if(a==-1){
                    robot[robotIdx][0]=i;
                    robot[robotIdx][1]=j;
                    robotIdx++;
                }
            }
        }

        spreadMap=new int[r][c];

        while(t-->0){
            spread();
            operate();
        }

        int sum=0;
        for(int i=0;i<r;i++){
            for(int j=0;j<c;j++){
                if(map[i][j]!=-1)sum+=map[i][j];
            }
        }
        System.out.println(sum);
    }

    static void spread(){
        for(int i=0;i<r;i++){
            for(int j=0;j<c;j++){
                int spreadCnt=0;
                if(map[i][j]>0){
                    for(int k=0;k<4;k++){
                        int ny=i+dy[k];
                        int nx=j+dx[k];
                        if(ny==-1 || nx==-1 || ny==r || nx==c)continue;
                        if(map[ny][nx]!=-1){
                            spreadMap[ny][nx]+=map[i][j]/5;
                            spreadCnt++;
                        }
                    }
                    map[i][j]=map[i][j]-map[i][j]/5*spreadCnt;
                }
            }
        }

        for(int i=0;i<r;i++){
            for(int j=0;j<c;j++){
                map[i][j]+=spreadMap[i][j];
            }
        }
        spreadMap=new int[r][c];
    }

    static void operate(){
        int top = robot[0][0];
        int bottom = robot[1][0];

        // 위쪽: 반시계 방향
        for (int i = top - 1; i > 0; i--) map[i][0] = map[i - 1][0];
        for (int i = 0; i < c - 1; i++) map[0][i] = map[0][i + 1];
        for (int i = 0; i < top; i++) map[i][c - 1] = map[i + 1][c - 1];
        for (int i = c - 1; i > 1; i--) map[top][i] = map[top][i - 1];
        map[top][1] = 0;

        // 아래쪽: 시계 방향
        for (int i = bottom + 1; i < r - 1; i++) map[i][0] = map[i + 1][0];
        for (int i = 0; i < c - 1; i++) map[r - 1][i] = map[r - 1][i + 1];
        for (int i = r - 1; i > bottom; i--) map[i][c - 1] = map[i - 1][c - 1];
        for (int i = c - 1; i > 1; i--) map[bottom][i] = map[bottom][i - 1];
        map[bottom][1] = 0;
    }

}
```
```java
//백준 이진 검색 트리
import java.io.*;
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int a=Integer.parseInt(br.readLine());
        Node root=new Node(a);
        while(true){
            String s=br.readLine();
            if(s==null || s.isEmpty())break;
            root.add(Integer.parseInt(s));
        }
        root.postOrder();
    }



    static class Node{
        int data;
        Node left=null;
        Node right=null;

        public Node(int data){
            this.data=data;
        }

        void add(int data){
            if(data<this.data){
                if(left==null){
                    left=new Node(data);
                    return ;
                }
                else{
                    left.add(data);
                }
            }
            else{
                if(right==null){
                    right=new Node(data);
                    return;
                }
                else right.add(data);
            }
        }

        void print(){
            System.out.println(this.data);
        }

        void postOrder(){
            if(left==null && right==null){
                print();
                return;
            }
            if(left!=null)left.postOrder();
            if(right!=null)right.postOrder();
            print();
        }
    }

}
```