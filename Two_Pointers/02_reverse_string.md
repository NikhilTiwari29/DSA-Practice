# 344. Reverse String

## Pattern
Two Pointers (Opposite Direction)

## Problem

Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array **in-place** with **O(1)** extra memory.

---

## Example 1

Input  
s = ["h","e","l","l","o"]

Output  
["o","l","l","e","h"]

---

## Example 2

Input  
s = ["H","a","n","n","a","h"]

Output  
["h","a","n","n","a","H"]

---

## Java Solution

```java
class Solution {

    public void reverseString(char[] s) {
        // bruteForceApproach(s);  // uses extra space
        optimisedApproach(s);      // in-place solution
    }

    // TC: O(n), SC: O(n)
    public void bruteForceApproach(char[] s) {
        ArrayList<Character> list = new ArrayList<>();

        // store in reverse
        for (int i = s.length - 1; i >= 0; i--) {
            list.add(s[i]);
        }

        // copy back
        for (int i = 0; i < s.length; i++) {
            s[i] = list.get(i);
        }
    }

    // TC: O(n), SC: O(1)
    public void optimisedApproach(char[] s) {
        int i = 0, j = s.length - 1;

        while (i < j) {
            // swap
            char temp = s[j];
            s[j] = s[i];
            s[i] = temp;

            i++;
            j--;
        }
    }
}
