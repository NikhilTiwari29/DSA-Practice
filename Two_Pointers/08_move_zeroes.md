# 283. Move Zeroes

## Pattern
Two Pointers (Fast & Slow)

## Problem

Given an integer array `nums`, move all `0`s to the end while maintaining the relative order of the non-zero elements.

You must do this in-place without making a copy of the array.

---

## Example 1

Input  
nums = [0,1,0,3,12]

Output  
[1,3,12,0,0]

---

## Example 2

Input  
nums = [0]

Output  
[0]

---

## Java Solution

```java
class Solution {
    public void moveZeroes(int[] nums) {
        // bruteForceApproach(nums);
        // betterApproach(nums);
        optimisedApproach(nums);
    }

    public void bruteForceApproach(int[] nums) {
        // TC: O(n^2)
        // SC: O(1)

        for (int i = 0; i < nums.length; i++) {
            for (int j = i; j < nums.length; j++) {
                if (nums[i] == 0 && nums[j] != 0){
                    int temp = nums[j];
                    nums[j] = nums[i];
                    nums[i] = temp;
                    break;
                }
            }
        }
    }

    public void betterApproach(int[] nums) {
        // TC: O(n)
        // SC: O(n)

        ArrayList<Integer> zeroList = new ArrayList<>();
        ArrayList<Integer> nonZeroList = new ArrayList<>();

        for (int num : nums) {
            if (num == 0) zeroList.add(num);
            else nonZeroList.add(num);
        }

        for (int i = 0; i < nonZeroList.size(); i++) {
            nums[i] = nonZeroList.get(i);
        }

        int index = 0;
        for (int i = nonZeroList.size(); i < nums.length; i++) {
            nums[i] = zeroList.get(index++);
        }
    }

    public void optimisedApproach(int[] nums) {
        // TC: O(n)
        // SC: O(1)

        int index = 0;

        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) {
                int temp = nums[i];
                nums[i] = nums[index];
                nums[index] = temp;
                index++;
            }
        }
    }
}
