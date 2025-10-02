```java
//프로그래머스 배열의 평균값
import java.util.Arrays;
class Solution {
    public double solution(int[] numbers) {
        double answer = Arrays.stream(numbers).average().orElse(0);
        return answer;
    }
}
```