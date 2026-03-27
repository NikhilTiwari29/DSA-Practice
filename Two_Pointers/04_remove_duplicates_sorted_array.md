# 26. Remove Duplicates from Sorted Array

## Pattern
Two Pointers (Fast & Slow)

## Problem

Given an integer array `nums` sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once.

Return the number of unique elements `k`.

The first `k` elements of `nums` should contain the unique elements in sorted order.

---

## Example 1

Input  
nums = [1,1,2]

Output  
2, nums = [1,2,_]

Explanation  
First two elements are unique. Remaining values can be ignored.

---

## Example 2

Input  
nums = [0,0,1,1,1,2,2,3,3,4]

Output  
5, nums = [0,1,2,3,4,_,_,_,_,_]

---

## Java Solution

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        // return bruteForceApproach(nums); //TC:-O(N) SC:- O(N)

        return optimisedApproach(nums); //TC:-O(N) SC:- O(1)
    }

    public int bruteForceApproach(int[] nums) {
        LinkedHashSet<Integer> hashSet = new LinkedHashSet<>();

        for (int i = 0; i < nums.length; i++) {
            hashSet.add(nums[i]);
        }

        int i = 0;
        for (int set : hashSet) {
            nums[i] = set;
            i++;
        }

        return hashSet.size();
    }

    public int optimisedApproach(int[] nums) {
        int i = 0;

        for (int j = 1; j < nums.length; j++) {
            if (nums[i] != nums[j]) {
                nums[i + 1] = nums[j];
                i++;
            }
        }

        return i + 1;
    }
}
