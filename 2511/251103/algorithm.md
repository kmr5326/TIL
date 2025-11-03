```java
//프로그래머스 주차 요금 계산
import java.util.*;
import java.time.*;
class Solution {
    public int[] solution(int[] fees, String[] records) {
        int[] answer = {};
        Set<String> carNums=new HashSet<>();
        Map<String,Long> parkedMin=new HashMap<>(); // 차량번호 : 주차시간
        Map<String,String> inTimeMap=new HashMap<>(); // 차량번호: 입차 시간
        
        for(int i=0;i<records.length;i++){
            String[] split=records[i].split(" ");
            carNums.add(split[1]);
            
            if(split[2].equals("IN")){
                inTimeMap.put(split[1],split[0]);
            }
            else {
                LocalTime in=LocalTime.parse(inTimeMap.get(split[1]));
                LocalTime out=LocalTime.parse(split[0]);
                Duration duration=Duration.between(in,out);
                
                long min=duration.toMinutes();
                parkedMin.put(split[1],parkedMin.getOrDefault(split[1],0L)+min);
                inTimeMap.remove(split[1]);
            }
        }
        
        for(String carNum:inTimeMap.keySet()){
            LocalTime in=LocalTime.parse(inTimeMap.get(carNum));
            LocalTime out=LocalTime.parse("23:59");
            Duration duration=Duration.between(in,out);

            long min=duration.toMinutes();
            parkedMin.put(carNum,parkedMin.getOrDefault(carNum,0L)+min);
        }
        
        
        List<String> sortedKey=new ArrayList<>(carNums);
        Collections.sort(sortedKey);
        answer=new int[sortedKey.size()];
        int idx=0;
        
        for(String carNum:sortedKey){
            long min=parkedMin.get(carNum);
            int fee=fees[1];
            if(min>fees[0]){
                int calMin=(int)Math.ceil((double)(min-fees[0])/fees[2]);
                fee+=calMin*fees[3];
            }
            answer[idx++]=fee;
        }
        
                
        return answer;
    }
}
```