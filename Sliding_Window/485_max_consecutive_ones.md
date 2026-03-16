# 485. Max Consecutive Ones

## Pattern
Array Traversal / Counting

## Problem

Given a binary array `nums`, return the maximum number of consecutive `1`s in the array.

---

## Example 1

Input  
nums = [1,1,0,1,1,1]

Output  
3

Explanation  
The first two digits or the last three digits are consecutive 1s.  
The maximum number of consecutive 1s is 3.

---

## Example 2

Input  
nums = [1,0,1,1,0,1]

Output  
2

---

## Java Solution

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        // return bruteForceApproach(nums); //TC:-O(N^2) SC:- O(1)

        return optimalApproach(nums); //TC:-O(N) SC:- O(1)
    }

    public int bruteForceApproach(int[] nums) {
        int maxCons = Integer.MIN_VALUE;

        for (int i = 0; i < nums.length; i++) {
            int count = 0;

            for (int j = i; j < nums.length; j++) {
                if (nums[j] == 1){
                    count++;
                } else {
                    break;
                }
            }

            maxCons = Math.max(maxCons, count);
        }

        return maxCons;
    }

    public int optimalApproach(int[] nums) {

        int maxCons = Integer.MIN_VALUE;
        int count = 0;

        for (int i = 0; i < nums.length; i++) {

            if (nums[i] == 1){
                count++;
            }
            else {
                maxCons = Math.max(maxCons, count);
                count = 0;
            }
        }

        maxCons = Math.max(maxCons, count);

        return maxCons;
    }
}
