```java
//백준 가희와 쓰레기 놀이
import java.io.*;
import java.util.*;
public class Main {
    static int o,e;
    static HashSet<CustomObject> objects;
    static HashMap<Integer,Connection> conMap;
    static HashMap<Integer,HashMap<Integer,Connection>> objIdMap; //objId, <refId,Con>
    static ArrayList<Integer> root;
    static HashSet<Integer> visit;

    public static void main(String[] args) throws IOException {
        BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st=new StringTokenizer(br.readLine());
        o=Integer.parseInt(st.nextToken());
        e=Integer.parseInt(st.nextToken());
        objects=new HashSet<>();
        conMap=new HashMap<>();
        objIdMap=new HashMap<>();
        root=new ArrayList<>();
        visit=new HashSet<>();
        for(int i=0;i<o;i++){
            st=new StringTokenizer(br.readLine());
            int num=Integer.parseInt(st.nextToken());
            String isRoot=st.nextToken();
            if(isRoot.equals("ROOT")){
                objects.add(new CustomObject(num,true));
                objIdMap.put(num,new HashMap<>());
                root.add(num);
            }
            else {
                objects.add(new CustomObject(num,false));
                objIdMap.put(num,new HashMap<>());
            }
        }

        for(int i=0;i<e;i++){
            st=new StringTokenizer(br.readLine());
            String cmd=st.nextToken();
            if(cmd.equals("MADE")){
                int num=Integer.parseInt(st.nextToken());
                String isRoot=st.nextToken();
                if(isRoot.equals("ROOT")){
                    objects.add(new CustomObject(num,true));
                    objIdMap.put(num,new HashMap<>());
                    root.add(num);
                }
                else {
                    objects.add(new CustomObject(num,false));
                    objIdMap.put(num,new HashMap<>());
                }
            }
            else if(cmd.equals("ADD")){
                int refId=Integer.parseInt(st.nextToken());
                int o1=Integer.parseInt(st.nextToken());
                String con=st.nextToken();
                int o2=Integer.parseInt(st.nextToken());
                if(con.equals("->")){
                    Connection conn=new Connection(refId,o1,o2,1);
                    conMap.put(refId,conn);
                    objIdMap.get(o1).put(refId,conn);
                    objIdMap.get(o2).put(refId,conn);
                }
                else{
                    Connection conn=new Connection(refId,o1,o2,2);
                    conMap.put(refId,conn);
                    objIdMap.get(o1).put(refId,conn);
                    objIdMap.get(o2).put(refId,conn);
                }
            }
            else if(cmd.equals("REMOVE")){
                int refId=Integer.parseInt(st.nextToken());
                Connection conn=conMap.get(refId);
                conMap.remove(refId);
                objIdMap.get(conn.from).remove(refId);
            }
            else if(cmd.equals("m")){
                visit=new HashSet<>();
                for(int r:root){
                    strongWeakConn(r);
                }
                removeObj();

                System.out.println(objects.size());
            }
            else if(cmd.equals("M")){
                visit=new HashSet<>();
                for(int r:root){
                    strongConn(r);
                }
                removeObj();

                System.out.println(objects.size());
            }
        }
    }

    static class CustomObject {
        int num;
        boolean isRoot;

        public CustomObject(int num, boolean isRoot){
            this.num=num;
            this.isRoot=isRoot;
        }

        @Override
        public boolean equals(Object o){
            if(this == o) return true;
            if(o == null || getClass() != o.getClass()) return false;
            CustomObject that = (CustomObject) o;
            return num == that.num;
        }

        @Override
        public int hashCode(){
            return Objects.hash(num);
        }
    }

    static class Connection{
        int id;
        int from;
        int to;
        int type; //1 약한 2 강한

        public Connection(int id,int from,int to,int type){
            this.id=id;
            this.from=from;
            this.to=to;
            this.type=type;
        }

    }

    static void strongWeakConn(int num){
        if(!objIdMap.containsKey(num)) return;
        HashMap<Integer,Connection> map=objIdMap.get(num);
        visit.add(num);
        for(Connection c: map.values()){
            if(!visit.contains(c.to)){
                strongWeakConn(c.to);
            }
        }
    }

    static void strongConn(int num){
        if(!objIdMap.containsKey(num)) return;
        HashMap<Integer,Connection> map=objIdMap.get(num);
        visit.add(num);
        for(Connection c: map.values()){
            if(!visit.contains(c.to) && c.type==2){
                strongConn(c.to);
            }
        }
    }

    static void removeObj(){
        Iterator<CustomObject> iter = objects.iterator();
        ArrayList<int[]> removeList=new ArrayList<>();
        while(iter.hasNext()){
            CustomObject o = iter.next();
            if(o.isRoot || visit.contains(o.num)) continue; // 반드시 ROOT 보호
            if(objIdMap.containsKey(o.num)){
                for(Connection c : objIdMap.get(o.num).values()){
                    removeList.add(new int[]{conMap.get(c.id).from,c.id});
                    removeList.add(new int[]{conMap.get(c.id).to,c.id});
                    conMap.remove(c.id);
                }
            }
            for(int[] e:removeList){
                if(objIdMap.containsKey(e[0]))objIdMap.get(e[0]).remove(e[1]);
            }
            objIdMap.remove(o.num);
            iter.remove();
        }
    }

}
```