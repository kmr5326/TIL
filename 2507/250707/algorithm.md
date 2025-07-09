```java
//프로그래머스 디스크 컨트롤러
import java.util.*;
class Solution {
    static PriorityQueue<Job> pq;
    static ArrayList<int[]> jobList;


    public int solution(int[][] jobs) {
        int answer = 0;
        int cnt=0;
        int sum=0;
        pq=new PriorityQueue<>();
        jobList=new ArrayList<>();

        for(int i=0;i< jobs.length;i++){
            jobList.add(new int[]{jobs[i][0],jobs[i][1],i});
        }

        jobList.sort((a,b)->{return a[0]!=b[0]?a[0]-b[0]:a[2]-b[2];});

        int idx=0;
        int time=jobList.get(0)[0];
        while(cnt!=jobs.length){
            while(idx<jobList.size() && jobList.get(idx)[0]<=time){
                int[] j=jobList.get(idx);
                pq.add(new Job(j[0],j[1],idx++));
            }

            if(!pq.isEmpty()){
                Job j=pq.poll();
                time=time+j.duration;
                sum+=time-j.requestTime;
                cnt++;
            }
            else time++;
        }


        answer=sum/cnt;
        return answer;
    }

    class Job implements Comparable<Job>{
        int requestTime;
        int duration;
        int num;

        public Job(int requestTime, int duration, int num){
            this.requestTime=requestTime;
            this.duration=duration;
            this.num=num;
        }

        public int compareTo(Job o){
            if(this.duration!=o.duration)return this.duration-o.duration;
            if(this.requestTime!=o.requestTime)return this.requestTime-o.requestTime;
            return this.num-o.num;
        }
    }
}
```