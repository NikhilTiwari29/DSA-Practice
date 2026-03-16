# 3. Longest Substring Without Repeating Characters

## Pattern
Sliding Window (Variable Size)  
No duplicate characters allowed

---

## Problem

Given a string `s`, find the length of the **longest substring without repeating characters**.

A substring must contain **contiguous characters**.

---

## Example 1

Input  
s = "abcabcbb"

Output  
3

Explanation  
The answer is `"abc"` with length **3**.  
Other valid substrings are `"bca"` and `"cab"`.

---

## Example 2

Input  
s = "bbbbb"

Output  
1

Explanation  
The answer is `"b"`.

---

## Example 3

Input  
s = "pwwkew"

Output  
3

Explanation  
The answer is `"wke"`.

Note: `"pwke"` is a **subsequence**, not a substring.

---

# Java Solution

```java
class Solution {

    public int lengthOfLongestSubstring(String s) {

        // return bruteForceApproach(s); // TC:- O(N²) SC:- O(N)

        return optimisedApproach(s); // TC:- O(N) SC:- O(N)
    }

    public int bruteForceApproach(String s) {

        int maxSize = 0;

        for (int i = 0; i < s.length(); i++) {

            HashSet<Character> hashSet = new HashSet<>();

            for (int j = i; j < s.length(); j++) {

                if (!hashSet.contains(s.charAt(j))){
                    hashSet.add(s.charAt(j));
                }
                else {
                    maxSize = Math.max(maxSize, hashSet.size());
                    break;
                }
            }

            maxSize = Math.max(maxSize, hashSet.size());
        }

        return maxSize;
    }

    public int optimisedApproach(String s) {

        int maxSize = 0;

        int i = 0;
        int j = 0;

        HashSet<Character> hashSet = new HashSet<>();

        while (j < s.length()){

            if (!hashSet.contains(s.charAt(j))){

                hashSet.add(s.charAt(j));

                maxSize = Math.max(maxSize, (j - i) + 1);

                j++;
            }
            else {

                hashSet.remove(s.charAt(i));

                i++;
            }
        }

        return maxSize;
    }
}
