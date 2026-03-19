# Max Consecutive Ones II

---

## 🧠 Pattern

**Sliding Window (Variable Size) + At Most K Violations**

---

## 📌 Problem

You are given a binary array `nums` containing only `0`s and `1`s.

You can flip **at most one `0`** to `1`.

Return the **maximum number of consecutive `1`s** possible after at most one flip.

---

## 🔍 Examples

### Example 1

```id="ex1"
Input: nums = [1, 0, 1, 1, 0]
Output: 4
Explanation: Flip first 0 → [1,1,1,1,0]
```

---

## 🔍 Key Insight

```text id="key1"
We need longest subarray with at most 1 zero
```

👉 Transform problem into:

```text id="key2"
Longest subarray with at most K violations (K = 1 zero)
```

---

# 🚀 Approaches

---

## 🧪 1. Brute Force

### 💡 Idea

* Try all subarrays
* Count number of zeros
* Stop if zeros > 1

---

### ⏱ Complexity

```text id="bf"
Time Complexity: O(N^2)
Space Complexity: O(1)
```

---

### 💻 Code

```java id="bfcode"
public int bruteForceApproach(int[] nums) {

    int maxLen = 0;

    for (int i = 0; i < nums.length; i++) {

        int zeroCount = 0;
        int currentLen = 0;

        for (int j = i; j < nums.length; j++) {

            if (nums[j] == 0) {
                zeroCount++;
            }

            // If more than 1 zero → invalid
            if (zeroCount > 1) {
                break;
            }

            currentLen++;
            maxLen = Math.max(maxLen, currentLen);
        }
    }

    return maxLen;
}
```

---

## ⚡ 2. Optimal (Sliding Window)

### 💡 Idea

```text id="opt1"
Expand → include elements  
Track zero count  
Shrink → when zero count > 1  
Track max length
```

---

### 🧠 Why It Works

* We maintain a window with **≤ 1 zero**
* This ensures we can flip at most one zero

---

### ⏱ Complexity

```text id="opt2"
Time Complexity: O(N)
- Each element is processed at most twice

Space Complexity: O(1)
```

---

### 💻 Code

```java id="optcode"
public int optimalApproach(int[] nums) {

    int left = 0;
    int zeroCount = 0;
    int maxLen = 0;

    for (int right = 0; right < nums.length; right++) {

        if (nums[right] == 0) {
            zeroCount++;
        }

        // Shrink window if more than 1 zero
        while (zeroCount > 1) {

            if (nums[left] == 0) {
                zeroCount--;
            }

            left++;
        }

        // Update max length
        maxLen = Math.max(maxLen, right - left + 1);
    }

    return maxLen;
}
```

---

## 🔁 Sliding Window Visualization

```id="vis"
[1,0,1,1,0]

→ [1,0,1,1] ✅ (1 zero)
→ add next → [1,0,1,1,0] ❌ (2 zeros)
→ shrink → [0,1,1,0] → valid
```

---

## ⚠️ Important Notes

* This is a **MAX problem**
* So:

```text id="rule1"
Shrink when INVALID (zeroCount > 1)
```

---

## 🧩 Pattern Summary

| Feature        | Value          |
| -------------- | -------------- |
| Window Type    | Variable       |
| Constraint     | At most 1 zero |
| Data Structure | Counter        |
| Expand         | Always         |
| Shrink         | While invalid  |
| Goal           | Max length     |

---

## 🔥 Golden Rule

```text id="rule2"
At most K violations → Sliding Window
```

---

## 🚀 Interview One-Liner

> “I convert this to finding the longest subarray with at most one zero, and use a sliding window with a counter to maintain the constraint.”

---

## 🎯 Final Takeaway

```text id="take"
At most K constraint → Sliding Window  
Track violations → shrink when invalid
```

---
