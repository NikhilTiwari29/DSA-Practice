# 75. Sort Colors

## Pattern
Two Pointers (Dutch National Flag)

## Problem

Given an array `nums` with values `0`, `1`, and `2` representing colors red, white, and blue respectively, sort them in-place so that same colors are adjacent.

You must solve it without using the library sort function.

---

## Example 1

Input  
nums = [2,0,2,1,1,0]

Output  
[0,0,1,1,2,2]

---

## Example 2

Input  
nums = [2,0,1]

Output  
[0,1,2]

---

## Java Solution

```java
class Solution {
    public void sortColors(int[] nums) {

        // TC = O(NlogN), SC = O(N)
        // mergeSortArr(nums,0,nums.length - 1);

        // ------------------------------------------------------------

        // TC = O(NlogN), SC = O(1)
        // quickSortMethod(nums, 0, nums.length - 1);

        // ------------------------------------------------------------

        // TC = O(2N), SC = O(1)
        // Counting approach

        // int zeroCount = 0, oneCount = 0, twoCount = 0;

        // for (int num : nums) {
        //     if (num == 0) zeroCount++;
        //     else if (num == 1) oneCount++;
        //     else twoCount++;
        // }

        // int index = 0;
        // for (int i = 0; i < zeroCount; i++) nums[index++] = 0;
        // for (int i = 0; i < oneCount; i++) nums[index++] = 1;
        // for (int i = 0; i < twoCount; i++) nums[index++] = 2;

        // --------------------------------------------------------------

        // TC = O(N), SC = O(1)
        // Dutch National Flag Algorithm

        int low = 0, mid = 0, high = nums.length - 1;

        while (mid <= high) {
            if (nums[mid] == 0) {
                swap(nums, low, mid);
                low++;
                mid++;
            }
            else if (nums[mid] == 1) {
                mid++;
            }
            else {
                swap(nums, mid, high);
                high--;
            }
        }
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
