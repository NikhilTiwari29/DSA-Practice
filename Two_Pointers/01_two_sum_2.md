# 167. Two Sum II - Input Array Is Sorted

## Pattern
Two Pointers (Opposite Direction)

## Problem

Given a 1-indexed array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific `target`.

Return the indices of the two numbers (1-based indexing).

---

## Example 1

Input  
numbers = [2,7,11,15], target = 9  

Output  
[1,2]  

Explanation  
The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2.

---

## Example 2

Input  
numbers = [2,3,4], target = 6  

Output  
[1,3]  

---

## Example 3

Input  
numbers = [-1,0], target = -1  

Output  
[1,2]  

---

## Java Solution

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {

        // Using optimal two-pointer approach
        // return bruteForceApproach(numbers, target);

        // Using optimal two-pointer approach
        return optimalApproach(numbers, target);
    }

    // Brute Force Approach
    // Time Complexity: O(n^2) → nested loops
    // Space Complexity: O(1) → no extra space used
    public int[] bruteForceApproach(int[] numbers, int target) {
        int[] ans = new int[2];

        for (int i = 0; i < numbers.length; i++) {
            for (int j = i + 1; j < numbers.length; j++) { // avoid same index
                if (numbers[i] + numbers[j] == target) {
                    ans[0] = i + 1; // 1-based indexing (LeetCode requirement)
                    ans[1] = j + 1;
                    break;
                }
            }
        }
        return ans;
    }

    // Optimal Two Pointer Approach (works because array is sorted)
    // Time Complexity: O(n) → each pointer moves at most once across array
    // Space Complexity: O(1) → no extra space used
    public int[] optimalApproach(int[] numbers, int target) {
        int i = 0;                     // left pointer (smallest element)
        int j = numbers.length - 1;    // right pointer (largest element)

        while (i < j) {
            int sum = numbers[i] + numbers[j];

            if (sum == target) {
                // Found the pair
                return new int[]{i + 1, j + 1}; // 1-based indexing
            } 
            else if (sum > target) {
                // Sum too large → move right pointer left to decrease sum
                j--;
            } 
            else {
                // Sum too small → move left pointer right to increase sum
                i++;
            }
        }

        return new int[]{-1, -1}; // fallback (problem guarantees one solution)
    }
}
