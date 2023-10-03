Original: [Count Triplets](https://www.hackerrank.com/challenges/count-triplets-1/problem)

## Problem
You are given an array and you need to find number of tripets of indices <i>(i,j,k)</i> such that the elements at those indices are in geometric progression for a given common ratio <i>r</i> and <i>i < j < k</i>.

## Code
```java
public class Solution {

    // Complete the countTriplets function below.
    static long countTriplets(List<Long> arr, long r) {
        long ans = 0;
        
        Map<Long, Long> mapForStart = new HashMap<>();
        Map<Long, Long> mapForMiddle = new HashMap<>();

        for (long num : arr) {
            if (num % r == 0) {
                long prev = num / r;
                Long cntForEnd = mapForMiddle.get(prev); // num is the last number

                if (cntForEnd != null) ans += cntForEnd;
                
                Long cntForMiddle = mapForStart.get(prev); // num is the middle number

                if (cntForMiddle != null) mapForMiddle.put(num, mapForMiddle.getOrDefault(num, 0L) + cntForMiddle);
            }
            
            mapForStart.put(num, mapForStart.getOrDefault(num, 0L) + 1); // num is the first number
        }

        return ans;
    }

    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] nr = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

        int n = Integer.parseInt(nr[0]);

        long r = Long.parseLong(nr[1]);

        List<Long> arr = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
            .map(Long::parseLong)
            .collect(toList());

        long ans = countTriplets(arr, r);

        bufferedWriter.write(String.valueOf(ans));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}
```
