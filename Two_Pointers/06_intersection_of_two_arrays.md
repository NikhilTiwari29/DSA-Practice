# 349. Intersection of Two Arrays

## Pattern
Two Pointers (Sorting + Traversal)

## Problem

Given two integer arrays `nums1` and `nums2`, return an array of their intersection.

Each element in the result must be unique, and you may return the result in any order.

---

## Example 1

Input  
nums1 = [1,2,2,1], nums2 = [2,2]

Output  
[2]

---

## Example 2

Input  
nums1 = [4,9,5], nums2 = [9,4,9,8,4]

Output  
[9,4]

---

## Java Solution

```java
import java.util.*;

class Solution {

    public int[] intersection(int[] nums1, int[] nums2) {

        // 🔴 Brute Force
        // return bruteForce(nums1, nums2);

        // 🟡 Better (HashSet)
        // return better(nums1, nums2);

        // 🔵 Two Pointer (Sorting)
        return twoPointer(nums1, nums2);
    }

    // 🔴 Brute Force
    public int[] bruteForce(int[] nums1, int[] nums2) {
        HashSet<Integer> set = new HashSet<>();

        for (int i = 0; i < nums1.length; i++) {
            for (int j = 0; j < nums2.length; j++) {
                if (nums1[i] == nums2[j]) {
                    set.add(nums2[j]);
                }
            }
        }

        return convertSetToArray(set);
    }

    // 🟡 Better (HashSet)
    public int[] better(int[] nums1, int[] nums2) {
        HashSet<Integer> set1 = new HashSet<>();
        HashSet<Integer> result = new HashSet<>();

        for (int num : nums1) {
            set1.add(num);
        }

        for (int num : nums2) {
            if (set1.contains(num)) {
                result.add(num);
            }
        }

        return convertSetToArray(result);
    }

    // 🔵 Two Pointer Approach
    public int[] twoPointer(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);

        int i = 0, j = 0;
        HashSet<Integer> set = new HashSet<>();

        while (i < nums1.length && j < nums2.length) {
            if (nums1[i] < nums2[j]) {
                i++;
            } else if (nums1[i] > nums2[j]) {
                j++;
            } else {
                set.add(nums1[i]);
                i++;
                j++;
            }
        }

        return convertSetToArray(set);
    }

    public int[] convertSetToArray(HashSet<Integer> set) {
        int[] result = new int[set.size()];
        int index = 0;

        for (int num : set) {
            result[index++] = num;
        }

        return result;
    }
}
