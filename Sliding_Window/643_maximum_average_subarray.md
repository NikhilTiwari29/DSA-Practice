# 643. Maximum Average Subarray I

## Pattern
Sliding Window (Fixed Size)

## Problem

You are given an integer array `nums` consisting of `n` elements, and an integer `k`.

Find a contiguous subarray whose length is equal to `k` that has the **maximum average value** and return this value. Any answer with a calculation error less than `10^-5` will be accepted.

---

## Example 1

Input  
nums = [1,12,-5,-6,50,3], k = 4  

Output  
12.75000  

Explanation  
Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75

---

## Example 2

Input  
nums = [5], k = 1  

Output  
5.00000

---

## Java Solution

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {

        // BRUTE FORCE APPROACH TC:- O(N*K) SC:- O(1)
        // return bruteForceApproach(nums, k);

        // OPTIMAL APPROACH TC:- O(N) SC:- O(1)
        return optimalApproach(nums, k);
    }

    public double bruteForceApproach(int[] nums, int k) {
        double maxAverage = Double.NEGATIVE_INFINITY;
        for (int i = 0; i < nums.length; i++) { // RUNS O(N) TIMES
            int count = 0;
            int sum = 0;

            for (int j = i; j < nums.length; j++) { // Runs at most O(K) times because the loop breaks when count == k
                if (count <= k){
                    sum = sum + nums[j];
                    count++;
                }

                if (count == k){
                    maxAverage = Math.max(maxAverage, (double) sum / k);
                    break;
                }
            }
        }
        return maxAverage;
    }

    public double optimalApproach(int[] nums, int k) {
        double maxAverage = Double.NEGATIVE_INFINITY;
        int sum = 0;

        for (int i = 0; i < k; i++) {
            sum += nums[i];
        }

        maxAverage = Math.max(maxAverage, (double) sum / k);

        for (int i = k; i < nums.length; i++) {
            sum += nums[i];
            sum -= nums[i - k];

            maxAverage = Math.max(maxAverage, (double) sum / k);
        }

        return maxAverage;
    }
}
