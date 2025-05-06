```java
//2차원 배열 회전 알고리즘
import java.io.*;
public class Main {

    public static void main(String[] args) throws IOException{
        int[][] arr=new int[5][5];
        int num=1;
        for(int i=0;i<5;i++){
            for(int j=0;j<5;j++)arr[i][j]=num++;
        }

        for(int i=0;i<5;i++){
            for(int j=0;j<5;j++) System.out.print(arr[i][j]+" ");
            System.out.println();
        }
        System.out.println();

        int[][] tmp=new int[5][5];
        int size=5;
        for(int i=0;i<5;i++){
            for(int j=0;j<5;j++)tmp[j][size-1-i]=arr[i][j];

        }

        for(int i=0;i<5;i++){
            for(int j=0;j<5;j++) System.out.print(tmp[i][j]+" ");
            System.out.println();
        }
        System.out.println();

        //반시계 90도 회전
        for(int i=0;i<5;i++){
            for(int j=0;j<5;j++)tmp[size-1-j][i]=arr[i][j];

        }

        for(int i=0;i<5;i++){
            for(int j=0;j<5;j++) System.out.print(tmp[i][j]+" ");
            System.out.println();
        }
    }

}
```
```java
//백준 톱니바퀴
import java.io.*;
import java.util.*;
public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int[][] gears=new int[4][8];
        for(int i=0;i<4;i++) {
            String str = br.readLine();
            for(int j=0;j<8;j++)gears[i][j]=str.charAt(j)-'0';
        }
        int k=Integer.parseInt(br.readLine());
        for(int i=0;i<k;i++){
            StringTokenizer st=new StringTokenizer(br.readLine());
            int num=Integer.parseInt(st.nextToken())-1;
            int dir=Integer.parseInt(st.nextToken());
            ArrayList<int[]> list;
            if(dir==1){
                list=rotate(gears,num,dir);
                forward(gears[num]);
            }
            else {
                list=rotate(gears,num,dir);
                backward(gears[num]);
            }
            for(int[] l:list){
                if(l[1]==1){
                    forward(gears[l[0]]);
                }
                else{
                    backward(gears[l[0]]);
                }
            }
        }
        int ans=0;
        for(int i=0;i<4;i++){
            if(gears[i][0]==1)ans+=(int)Math.pow(2,i);
        }
        System.out.println(ans);
    }

    static void forward(int[] gear){
        int tmp=gear[7];
        for(int i=7;i>0;i--)gear[i]=gear[i-1];
        gear[0]=tmp;
    }

    static void backward(int[] gear){
        int tmp=gear[0];
        for(int i=0;i<7;i++)gear[i]=gear[i+1];
        gear[7]=tmp;
    }

    static ArrayList<int[]> rotate(int[][] gears,int num,int dir){
        ArrayList<int[]> list=new ArrayList<>();
        int idx=num+1;
        int originDir=dir;
        while(idx<4){
            if(gears[idx-1][2]!=gears[idx][6]){
                if(dir==1){
                    list.add(new int[]{idx,dir*-1});
                    dir=-1;
                }
                else{
                    list.add(new int[]{idx,dir*-1});
                    dir=1;
                }
            }
            else break;
            idx++;
        }
        idx=num-1;
        dir=originDir;
        while(idx>-1){
            if(gears[idx+1][6]!=gears[idx][2]){
                if(dir==1){
                    list.add(new int[]{idx,dir*-1});
                    dir=-1;
                }
                else{
                    list.add(new int[]{idx,dir*-1});
                    dir=1;
                }
            }
            else break;
            idx--;
        }
        return list;
    }

}
```