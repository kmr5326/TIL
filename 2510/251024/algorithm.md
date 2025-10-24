```java
//프로그래머스 합승 택시 요금
import java.util.*;
class Solution {
    static Map<Integer,List<Edge>> edges;

    public int solution(int n, int s, int a, int b, int[][] fares) {
        int answer = 0;
        edges=new HashMap<>();

        for(int[] f:fares){
            int c=f[0],d=f[1],cost=f[2];
            if(!edges.containsKey(c))edges.put(c,new ArrayList<>());
            if(!edges.containsKey(d))edges.put(d,new ArrayList<>());
            edges.get(c).add(Edge.of(d,cost));
            edges.get(d).add(Edge.of(c,cost));
        }
        int[] distS=dijk(s,n);
        int[] distA=dijk(a,n);
        int[] distB=dijk(b,n);
        answer=distS[a]+distS[b];
        for(int i=1;i<=n;i++){
            if(i==s)continue;
            if(distS[i]==Integer.MAX_VALUE || distA[i]==Integer.MAX_VALUE || distB[i]==Integer.MAX_VALUE)continue;
            answer=Math.min(answer,distS[i]+distA[i]+distB[i]);
        }
        return answer;
    }

    int[] dijk(int s,int n){
        int[] dist=new int[n+1];
        Arrays.fill(dist,Integer.MAX_VALUE);
        dist[s]=0;
        PriorityQueue<Node> pq=new PriorityQueue<>();
        pq.add(new Node(s,0));

        while(!pq.isEmpty()){
            Node now=pq.poll();
            if(now.cost>dist[now.num])continue;
            for(Edge e:edges.getOrDefault(now.num,new ArrayList<>())){
                if(dist[e.to]>now.cost+e.cost){
                    dist[e.to]=now.cost+e.cost;
                    pq.add(new Node(e.to,dist[e.to]));
                }
            }
        }
        return dist;
    }

    static class Edge{
        int to;
        int cost;

        Edge(int to,int c){
            this.to=to;
            this.cost=c;
        }

        public static Edge of(int to,int c){
            return new Edge(to,c);
        }
    }

    static class Node implements Comparable<Node>{
        int num;
        int cost;

        Node(int n,int c){
            num=n;
            cost=c;
        }

        public int compareTo(Node o){
            return this.cost-o.cost;
        }
    }
}
```