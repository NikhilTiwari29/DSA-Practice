# 27. Remove Element

## Pattern
Two Pointers (Fast & Slow)

## Problem

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in-place.

Return the number of elements `k` that are not equal to `val`.

The first `k` elements of `nums` should contain the valid elements. The remaining elements can be ignored.

---

## Example 1

Input  
nums = [3,2,2,3], val = 3  

Output  
2, nums = [2,2,_,_]

---

## Example 2

Input  
nums = [0,1,2,2,3,0,4,2], val = 2  

Output  
5, nums = [0,1,4,0,3,_,_,_]

---

## Java Solution

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        // return bruteForceApproach(nums,val);
        return optimisedApproach(nums,val);
    }

    public int bruteForceApproach(int[] nums, int val) {
        ArrayList<Integer> list = new ArrayList<>();

        // TC: O(n)
        // SC: O(n)
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val){
                list.add(nums[i]);
            }
        }

        for (int i = 0; i < list.size(); i++) {
            nums[i] = list.get(i);
        }

        return list.size();
    }

    public int optimisedApproach(int[] nums, int val) {
        int index = 0;

        // TC: O(n)
        // SC: O(1)
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val){
                nums[index] = nums[i];
                index++;
            }
        }

        return index;
    }
}
