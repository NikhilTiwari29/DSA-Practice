# 209. Minimum Size Subarray Sum

---

## 🧠 Pattern

**Sliding Window (Variable Size)**

---

## 📌 Problem

Given an array of **positive integers** `nums` and a positive integer `target`,
return the **minimal length of a subarray** whose sum is **greater than or equal to target**.

If there is no such subarray, return `0`.

---

## 🧾 Constraints

* `1 <= target <= 10^9`
* `1 <= nums.length <= 10^5`
* `1 <= nums[i] <= 10^4`

---

## 🔍 Examples

### Example 1

```id="n4z5os"
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: [4,3]
```

---

### Example 2

```id="t9zjka"
Input: target = 4, nums = [1,4,4]
Output: 1
```

---

### Example 3

```id="d2is4j"
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```

---

## 🔍 Key Insight

```text id="s6p0j3"
All elements are POSITIVE → sum is monotonic
```

👉 This allows us to use **Sliding Window**

---

## 🚀 Approaches

---

## 🧪 1. Brute Force

### 💡 Idea

* Try every subarray
* Track sum
* Update minimum length

---

### ⏱ Complexity

```text id="n6o6a0"
Time Complexity: O(N^2)
Space Complexity: O(1)
```

---

### 💻 Code

```java id="p5m4ho"
public int bruteForceApproach(int target, int[] nums) {

    int minSize = Integer.MAX_VALUE;

    for (int i = 0; i < nums.length; i++) {

        int sum = 0;

        for (int j = i; j < nums.length; j++) {

            sum += nums[j];

            if (sum >= target) {
                minSize = Math.min(minSize, (j - i) + 1);
            }
        }
    }

    return minSize == Integer.MAX_VALUE ? 0 : minSize;
}
```

---

## ⚡ 2. Optimal (Sliding Window)

### 💡 Idea

```text id="tq2r8u"
Expand → until sum >= target  
Shrink → while sum >= target (to minimize length)
```

---

### 🧠 Why It Works

* All numbers are **positive**
* Sum increases on expansion, decreases on shrinking
* Window behaves predictably

---

### ⏱ Complexity

```text id="5hzx4h"
Time Complexity: O(N)
- Each element is added once and removed once → 2N

Space Complexity: O(1)
```

---

### 💻 Code

```java id="6g7j2z"
public int optimalApproach(int target, int[] nums) {

    int minSize = Integer.MAX_VALUE;
    int sum = 0;
    int left = 0;

    for (int right = 0; right < nums.length; right++) {

        // Expand window
        sum += nums[right];

        // Shrink window while valid
        while (sum >= target) {

            // Update answer BEFORE shrinking
            minSize = Math.min(minSize, right - left + 1);

            sum -= nums[left];
            left++;
        }
    }

    return minSize == Integer.MAX_VALUE ? 0 : minSize;
}
```

---

## 🔁 Sliding Window Visualization

```id="9j2f7y"
target = 7

[2,3,1,2] → sum = 8 ✅ (length 4)
shrink → [3,1,2] → sum = 6 ❌

continue...

[4,3] → sum = 7 ✅ (length 2) ⭐
```

---

## ⚠️ Important Notes

* Works **only for positive numbers**
* If negatives exist → ❌ Sliding window fails
  → use **Prefix Sum**

---

## 🧩 Pattern Summary

| Feature     | Value          |
| ----------- | -------------- |
| Window Type | Variable       |
| Expand      | Always         |
| Shrink      | While valid    |
| Goal        | Minimum length |

---

## 🔥 Golden Rule

```text id="k6t7sj"
MIN problem → update → shrink
```

---

## 🚀 Interview One-Liner

> “Since all elements are positive, I use a sliding window where I expand to reach the target sum and shrink the window to find the minimum length.”

---

## 🎯 Final Takeaway

```text id="4v4nfw"
Positive numbers + sum constraint + minimum length  
→ Sliding Window (Shrink while VALID)
```

---
