```java
//프로그래머스 베스트앨범
import java.util.*;
class Solution {
    static HashMap<String,Integer> playsTotal;
    static HashMap<String,PriorityQueue<Song>> genreSong;
    
    public int[] solution(String[] genres, int[] plays) {
        int n=plays.length;
        
        playsTotal=new HashMap<>();
        genreSong=new HashMap<>();
        
        for(int i=0;i<n;i++){
            if(!playsTotal.containsKey(genres[i]))playsTotal.put(genres[i],plays[i]);
            else playsTotal.put(genres[i],playsTotal.get(genres[i])+plays[i]);
            
            if(!genreSong.containsKey(genres[i])){
                genreSong.put(genres[i],new PriorityQueue<>());
            }
            genreSong.get(genres[i]).add(new Song(i,plays[i]));
        }
        
        PriorityQueue<Genre> genrePq=new PriorityQueue<>();
        for(String s:playsTotal.keySet()){
            genrePq.add(new Genre(s,playsTotal.get(s)));
        }
        
        int idx=0;
        int cnt=0;
        ArrayList<Integer> ans=new ArrayList<>();
        while(!genrePq.isEmpty()){
            Genre g=genrePq.poll();
            PriorityQueue<Song> songPq=genreSong.get(g.name);
            while(!songPq.isEmpty()){
                if(cnt==2){
                    cnt=0;
                    break;
                }
                ans.add(songPq.poll().num);
                cnt++;
            }
            cnt=0;
        }
        int[] answer = ans.stream().mapToInt(Integer::intValue).toArray();
        return answer;
    }
    
    static class Song implements Comparable<Song>{
        int num;
        int plays;
        
        public Song(int num,int plays){
            this.num=num;
            this.plays=plays;
        }
        
        @Override
        public int compareTo(Song o){
            if(this.plays==o.plays)return this.num-o.num;
            else return o.plays-this.plays;
        }
    }
    
    static class Genre implements Comparable<Genre>{
        String name;
        int plays;
        
        public Genre(String name,int plays){
            this.name=name;
            this.plays=plays;
        }
        
        @Override
        public int compareTo(Genre o){
            return o.plays-this.plays;
        }
    }
}
```