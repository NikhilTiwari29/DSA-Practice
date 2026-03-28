# 680. Valid Palindrome II

## Pattern
Two Pointers (Opposite Direction)

## Problem

Given a string `s`, return `true` if the string can be a palindrome after deleting at most one character.

---

## Example 1

Input  
s = "aba"

Output  
true  

---

## Example 2

Input  
s = "abca"

Output  
true  

Explanation  
You can delete 'c' to make it a palindrome.

---

## Example 3

Input  
s = "abc"

Output  
false  

---

## Java Solution

```java
class Solution {
    public boolean validPalindrome(String s) {

        int i = 0;
        int j = s.length() - 1;

        // TC: O(n)
        // SC: O(1)
        while (i < j){
            if (s.charAt(i) == s.charAt(j)){
                i++;
                j--;
            }
            else {
                // Try skipping either left or right character
                return isValidPalindrome(s, i + 1, j) 
                    || isValidPalindrome(s, i, j - 1);
            }
        }

        return true;
    }

    private static boolean isValidPalindrome(String s, int i, int j) {

        while (i < j){
            if (s.charAt(i) == s.charAt(j)){
                i++;
                j--;
            }
            else {
                return false;
            }
        }
        return true;
    }
}
