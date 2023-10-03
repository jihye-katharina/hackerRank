Original: [Max Array Sum](https://www.hackerrank.com/challenges/max-array-sum/problem)

## Problem
Given an array of integers, find the subset of non-adjacent elements with the maximum sum. Calculate the sum of that subset. It is possible that the maximum sum is <i>0</i>, the case when all elements are negative.

## Code
```java
public class Solution {

    // Complete the maxSubsetSum function below.
    static int maxSubsetSum(int[] arr) {
        int max = 0;
        int[] dp = new int[arr.length + 1];

        dp[0] = 0;
        dp[1] = arr[0];
        dp[2] = arr[1];

        for (int i = 3; i <= arr.length; i++) {
            int tmp = Math.max(dp[i-2], dp[i-3]);

            if (0 <= arr[i-1]) dp[i] = Math.max(arr[i-1], tmp + arr[i-1]);
            else dp[i] = tmp;
            
            max = Math.max(max, dp[i]);
        }

        return max;
    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) throws IOException {
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int n = scanner.nextInt();
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        int[] arr = new int[n];

        String[] arrItems = scanner.nextLine().split(" ");
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        for (int i = 0; i < n; i++) {
            int arrItem = Integer.parseInt(arrItems[i]);
            arr[i] = arrItem;
        }

        int res = maxSubsetSum(arr);

        bufferedWriter.write(String.valueOf(res));
        bufferedWriter.newLine();

        bufferedWriter.close();

        scanner.close();
    }
}
```
