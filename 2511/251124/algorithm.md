```java
//프로그래머스 길 찾기 게임
import java.util.*;
class Solution {
    int idx;
    
    public int[][] solution(int[][] nodeinfo) {
        int[][] answer = {};
        
        Node[] nodes=new Node[nodeinfo.length];
        for(int i=0;i<nodeinfo.length;i++){
            nodes[i]=new Node(i+1,nodeinfo[i][0],nodeinfo[i][1]);
        }
        
        Arrays.sort(nodes, (a,b)->{
            if(a.y!=b.y)return b.y-a.y;
            else return a.x-b.x;
        });
            
        
        Node root=nodes[0];
        
        for(int i=1;i<nodes.length;i++){
            insert(root,nodes[i]);
        }
        
        answer=new int[2][nodes.length];
        idx=0;
        preorder(root,answer);
        idx=0;
        postorder(root,answer);
        
        return answer;
    }
    
    class Node{
        int num;
        int x,y;
        Node lChild;
        Node rChild;
        
        Node(int num,int x,int y){
            this.num=num;
            this.x=x;
            this.y=y;
            this.lChild=null;
            this.rChild=null;
        }
    }
    
    void insert(Node parent,Node child){
        if(parent.x>child.x){
            if(parent.lChild==null)parent.lChild=child;
            else insert(parent.lChild,child);
        }
        else{
            if(parent.rChild==null)parent.rChild=child;
            else insert(parent.rChild,child);
        }
    }
    
    void preorder(Node node,int[][] answer){
        if(node!=null){
            answer[0][idx++]=node.num;
            preorder(node.lChild,answer);
            preorder(node.rChild,answer);
        }
    }
    
    void postorder(Node node,int[][] answer){
        if(node!=null){
            postorder(node.lChild,answer);
            postorder(node.rChild,answer);
            answer[1][idx++]=node.num;
        }
    }
}
```