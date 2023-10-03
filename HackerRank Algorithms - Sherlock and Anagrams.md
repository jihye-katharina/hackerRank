Original: [Sherlock and Anagrams](https://www.hackerrank.com/challenges/sherlock-and-anagrams/problem)


## Problem
Two strings are anagrams of each other if the letters of one string can be rearranged to form the other string. Given a string, find the number of pairs of substrings of the string that are anagrams of each other.

## Code
```java
class Result {

    /*
     * Complete the 'sherlockAndAnagrams' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts STRING s as parameter.
     */

    static boolean isAnagrams(String s1, String s2) {
        if (s1.length() != s2.length()) return false;
        
        int cnt = 0;
        boolean[] visit = new boolean[s2.length()];

        for (int i = 0; i < s1.length(); i++) {
            for (int j = 0; j < s2.length(); j++) {
                if (s1.charAt(i) == s2.charAt(j) && !visit[j]) {
                    cnt++; visit[j] = true; break;
                }
            }
        }

        return cnt == s2.length()? true : false;
    }

    static int sherlockAndAnagrams(String s) {
        List<String> list = new ArrayList<>();

        for (int i = 0; i < s.length(); i++) {
            for (int j = i + 1; j <= s.length(); j++) 
                list.add(s.substring(i, j));
        }
        
        int ans = 0;

        for (int i = 0; i < list.size(); i++) {
            for (int j = i + 1; j < list.size(); j++) {
                if (isAnagrams(list.get(i), list.get(j))) ans++;
            }
        }

        return ans;
    }
}
```
