```java
//프로그래머스 교점에 별 만들기
import java.util.*;
class Solution {
    public String[] solution(int[][] line) {
        List<long[]> points = new ArrayList<>();
        long minX = Long.MAX_VALUE, maxX = Long.MIN_VALUE;
        long minY = Long.MAX_VALUE, maxY = Long.MIN_VALUE;

        int n = line.length;
        for (int i = 0; i < n; i++) {
            long a = line[i][0], b = line[i][1], e = line[i][2];
            for (int j = i + 1; j < n; j++) {
                long c = line[j][0], d = line[j][1], f = line[j][2];

                long denom = a * d - b * c;      // ad - bc
                if (denom == 0) continue;        // 평행 또는 일치

                long xNum = b * f - e * d;       // bf - ed
                long yNum = e * c - a * f;       // ec - af

                // 정수 좌표인지 확인
                if (xNum % denom != 0 || yNum % denom != 0) continue;

                long x = xNum / denom;
                long y = yNum / denom;

                points.add(new long[]{y, x});
                minX = Math.min(minX, x);
                maxX = Math.max(maxX, x);
                minY = Math.min(minY, y);
                maxY = Math.max(maxY, y);
            }
        }

        int H = (int) (maxY - minY + 1);
        int W = (int) (maxX - minX + 1);
        char[][] board = new char[H][W];
        for (int i = 0; i < H; i++) Arrays.fill(board[i], '.');

        for (long[] p : points) {
            long y = p[0], x = p[1];
            int r = (int) (maxY - y);   // y 큰 값이 위(0행)
            int c = (int) (x - minX);
            board[r][c] = '*';
        }

        String[] ans = new String[H];
        for (int i = 0; i < H; i++) ans[i] = new String(board[i]);
        return ans;
    }
}
```