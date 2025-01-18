# Longest Substring with At Most K Distinct Characters
https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters

Given a string s and an integer k, return the length of the longest substring of s that contains at most k distinct characters.
```java
Example 1:

Input: s = "eceba", k = 2
Output: 3
Explanation: The substring is "ece" with length 3.

Example 2:

Input: s = "aa", k = 1
Output: 2
Explanation: The substring is "aa" with length 2.
``` 

## Constraints:

1. 1 <= s.length <= 5 * 10^4
2. 0 <= k <= 50

## Implementation : Sliding Window
```java
class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        int n = s.length();
        if (n <= k) return n;

        int left = 0, right = 0;
        HashMap<Character, Integer> hashmap = new HashMap<Character, Integer>();
        int max_len = k;
        while (right < n) {
            hashmap.put(s.charAt(right), right);
            if (hashmap.size() > k) {
                int del_idx = Collections.min(hashmap.values());
                hashmap.remove(s.charAt(del_idx));
                left = del_idx + 1;
            }
            max_len = Math.max(max_len, right - left + 1);
            right++;
        }
        return max_len;
    }
}
```

## Note : Taking k=2 as example
In above implementation, when updating the left pointer, **make sure you are deleting the least recent character.**

It would be wrong to delete the recent occurrence of character pointed by left pointer, character at left may not be the least recent one.

e.g. {1,2,1,2,1,3,3,3,3,3}, **when seeing value 3, we should delete value 2 (because that was the least recent from 3 values in the map), and we should move the left pointer to point to 1.**

So answer in this case would be 6.

## References :
https://github.com/eMahtab/longest-substring-with-at-most-two-distinct-characters
