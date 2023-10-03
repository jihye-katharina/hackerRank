Original: [Greedy Florist](https://www.hackerrank.com/challenges/greedy-florist/problem?h_r=internal-search)

## Problem
A group of friends want to buy a bouquet of flowers. The florist wants to maximize his number of new customers and the money he makes. To do this, he decides he'll multiply the price of each flower by the number of that customer's previously purchased flowers plus <i>1</i>. The first flower will be original price, <i>(0 + 1) * original price</i> , the next will be <i>(1 + 1) * original price</i> and so on.

Given the size of the group of friends, the number of flowers they want to purchase and the original prices of the flowers, determine the minimum cost to purchase all of the flowers. The number of flowers they want equals the length of the <i>c</i> array.


## Code
```java
public class Solution {

    // Complete the getMinimumCost function below.
    static int getMinimumCost(int k, int[] c) {
        int[] friends = new int[k];

        for (int i = 0; i < k; i++) friends[i] = c.length / k;
        for (int i = 0; i < c.length % k; i++) friends[i] += 1;
        
        Arrays.sort(c);

        int sum = 0, idx = 0;

        while (idx < c.length) {
            for (int j = 0; j < k; j++) {
                if (friends[j] > 0) sum += (--friends[j] + 1) * c[idx++];
            }
        }

        return sum;
    }

    private static final Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) throws IOException {
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] nk = scanner.nextLine().split(" ");

        int n = Integer.parseInt(nk[0]);

        int k = Integer.parseInt(nk[1]);

        int[] c = new int[n];

        String[] cItems = scanner.nextLine().split(" ");
        scanner.skip("(\r\n|[\n\r\u2028\u2029\u0085])?");

        for (int i = 0; i < n; i++) {
            int cItem = Integer.parseInt(cItems[i]);
            c[i] = cItem;
        }

        int minimumCost = getMinimumCost(k, c);

        bufferedWriter.write(String.valueOf(minimumCost));
        bufferedWriter.newLine();

        bufferedWriter.close();

        scanner.close();
    }
}
