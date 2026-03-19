# 209. Minimum Size Subarray Sum

## Pattern
Sliding Window (Variable Size)

## Problem

Given an array of positive integers `nums` and a positive integer `target`, return the **minimal length of a subarray whose sum is greater than or equal to target**.

If there is no such subarray, return `0` instead.

---

## Example 1

Input  
target = 7, nums = [2,3,1,2,4,3]

Output  
2

Explanation  
The subarray `[4,3]` has the minimal length under the problem constraint.

---

## Example 2

Input  
target = 4, nums = [1,4,4]

Output  
1

---

## Example 3

Input  
target = 11, nums = [1,1,1,1,1,1,1,1]

Output  
0

---

# Java Solution

```java
class Solution {

    public int minSubArrayLen(int target, int[] nums) {

        // return bruteForceApproach(target, nums); // TC:- O(N^2) SC:- O(1)

        return optimalApproach(target, nums); // TC:- O(2N) = O(N) SC:- O(1)
    }

    public int bruteForceApproach(int target, int[] nums) {

        int minSize = Integer.MAX_VALUE;

        for (int i = 0; i < nums.length; i++) {

            int sum = 0;

            for (int j = i; j < nums.length; j++) {

                sum += nums[j];

                if (sum >= target) {

                    int length = (j - i) + 1;

                    minSize = Math.min(minSize, length);
                }
            }
        }

        if (minSize == Integer.MAX_VALUE) minSize = 0;

        return minSize;
    }

    public int optimalApproach(int target, int[] nums) {

        int minSize = Integer.MAX_VALUE;
        int sum = 0;
        int startPos = 0;

        for (int i = 0; i < nums.length; i++) {

            sum += nums[i];

            while (sum >= target) { 
                // This while loop doesn't run N times for each iteration,
                // so overall complexity remains O(N)

                int length = (i - startPos) + 1;

                minSize = Math.min(minSize, length);

                sum -= nums[startPos];
                startPos++;
            }
        }

        if (minSize == Integer.MAX_VALUE) minSize = 0;

        return minSize;
    }
}
