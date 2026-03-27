# 125. Valid Palindrome

## Pattern
Two Pointers (Opposite Direction)

## Problem

A phrase is a palindrome if, after converting all uppercase letters into lowercase and removing all non-alphanumeric characters, it reads the same forward and backward.

Given a string `s`, return `true` if it is a palindrome, otherwise `false`.

---

## Example 1

Input  
s = "A man, a plan, a canal: Panama"

Output  
true  

Explanation  
"amanaplanacanalpanama" is a palindrome.

---

## Example 2

Input  
s = "race a car"

Output  
false  

---

## Example 3

Input  
s = " "

Output  
true  

Explanation  
After removing non-alphanumeric characters → "" (empty string), which is a palindrome.

---

## Java Solution

```java
class Solution {
    public boolean isPalindrome(String s) {

        // return bruteForceApproach(s);

        return optimisedApproach(s);
    }

    public boolean bruteForceApproach(String s) {

        s = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();

        if (s.length() == 0) return true;

        StringBuilder ansTemp = new StringBuilder();

        for (int i = s.length() - 1; i >= 0; i--) {
            ansTemp.append(s.charAt(i));
        }

        String ans = ansTemp.toString();

        if (s.equals(ans)){
            return true;
        }

        return false;
    }

    public boolean optimisedApproach(String s) {

        int i = 0, j = s.length() - 1;

        // TC: O(n)
        // SC: O(1)
        while (i < j) {

            // skip non-alphanumeric from left
            while (i < j && !Character.isLetterOrDigit(s.charAt(i))) {
                i++;
            }

            // skip non-alphanumeric from right
            while (i < j && !Character.isLetterOrDigit(s.charAt(j))) {
                j--;
            }

            // compare after converting to lowercase
            if (Character.toLowerCase(s.charAt(i)) != Character.toLowerCase(s.charAt(j))) {
                return false;
            }

            i++;
            j--;
        }

        return true;
    }
}
