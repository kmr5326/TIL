```java
//프로그래머스 표 편집
import java.util.*;
class Solution {
    public String solution(int n, int k, String[] cmd) {
        String answer = "";
        List<Node> nodes=new ArrayList<>();
        Stack<Integer> rmStack=new Stack<>();
        
        for(int i=0;i<n;i++){
            Node node;
            if(i==0){
                node=new Node(i,null,null,true,false);
            }
            else if(i==n-1){
                Node prev = nodes.get(i-1);
                node=new Node(i,prev,null,false,true);
                prev.next=node;
            }
            else {
                Node prev = nodes.get(i-1);
                node = new Node(i,prev,null,false,false); 
                prev.next=node;
            }
            nodes.add(node);
        }
        
        Node current=nodes.get(k);
        
        for(String c: cmd){
            if(c.equals("C")){
                current.remove();
                rmStack.add(current.idx);
                if(current.isTail()){    
                    current=current.previous;
                }
                else {
                    current=current.next;
                }
            }
            else if(c.equals("Z")){
                Node recoveryNode = nodes.get(rmStack.pop());
                recoveryNode.recovery();
            } 
            else{
                String[] s=c.split(" ");
                int move=Integer.parseInt(s[1]);
                if(s[0].equals("U")){
                    for(int i=0;i<move;i++)current=current.previous;
                }
                else for(int i=0;i<move;i++)current=current.next;
            }
        }
        
        StringBuilder sb= new StringBuilder();
        
        for(Node node:nodes){
            if(node.isDeleted())sb.append("X");
            else sb.append("O");
        }
        answer=sb.toString();
        return answer;
    }
    
    class Node{
        int idx;
        boolean head;
        boolean tail;
        Node previous;
        Node next;
        boolean deleted=false;
        
        boolean isHead(){
            return this.head;
        }
        
        boolean isTail(){return this.tail;}
        
        Node(int i,Node previous,Node next, boolean head,boolean tail){
            this.idx=i;
            this.previous=previous;
            this.next=next;
            this.head=head;
            this.tail=tail;
        }
        
        void remove(){
            if(isHead()){
                this.next.head=true;
                this.next.previous=null;
                this.deleted=true;
                return;
            }
            if(isTail()){
                this.previous.tail=true;
                this.previous.next=null;
                this.deleted=true;
                return;
            }
            this.previous.next=this.next;
            this.next.previous=this.previous;
            this.deleted=true;
        }
        
        boolean isDeleted(){return this.deleted;}
        
        void recovery(){
            this.deleted=false;
            if(isHead()){
                this.next.previous=this;
                this.next.head=false;
                return;
            }
            if(isTail()){
                this.previous.next=this;
                this.previous.tail=false;
                return;
            }
            this.previous.next=this;
            this.next.previous=this;
        }
    }
}
```