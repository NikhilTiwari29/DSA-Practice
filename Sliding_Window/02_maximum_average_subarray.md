# 643. Maximum Average Subarray I

---

## 🧠 Pattern

**Sliding Window (Fixed Size)**

---

## 📌 Problem

You are given an integer array `nums` consisting of `n` elements, and an integer `k`.

Find a **contiguous subarray whose length is equal to `k`** that has the **maximum average value** and return this value.

Any answer with a calculation error less than `10^-5` will be accepted.

---

## 🧾 Constraints

* `n == nums.length`
* `1 <= k <= n <= 10^5`
* `-10^4 <= nums[i] <= 10^4`

---

## 🔍 Examples

### Example 1

```
Input: nums = [1,12,-5,-6,50,3], k = 4
Output: 12.75000
Explanation:
Maximum average = (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
```

---

### Example 2

```
Input: nums = [5], k = 1
Output: 5.00000
```

---

## 🔍 Key Insight

```text id="xtxiqo"
Since k is FIXED → maximizing average = maximizing sum
```

👉 So we only need to track **maximum sum of size k window**

---

# 🚀 Approaches

---

## 🧪 1. Brute Force

### 💡 Idea

* Try every subarray of size `k`
* Compute sum each time

---

### ⏱ Complexity

```text id="a8yd8k"
Time Complexity: O(N * K)
- Outer loop runs N times
- Inner loop runs K times

Space Complexity: O(1)
```

---

### 💻 Code

```java id="tpmkoi"
public double bruteForceApproach(int[] nums, int k) {

    double maxAverage = Double.NEGATIVE_INFINITY;

    for (int i = 0; i < nums.length; i++) {

        int sum = 0;
        int count = 0;

        for (int j = i; j < nums.length; j++) {

            sum += nums[j];
            count++;

            if (count == k) {
                maxAverage = Math.max(maxAverage, (double) sum / k);
                break;
            }
        }
    }

    return maxAverage;
}
```

---

## ⚡ 2. Optimal (Sliding Window)

### 💡 Idea

```text id="fkjdus"
Reuse previous window sum
```

```text id="zvyqei"
New window = old window + next element - previous element
```

---

### 🧠 Why It Works

* Window size is **fixed (k)**
* Each step takes **O(1)** time

---

### ⏱ Complexity

```text id="8qk0k7"
Time Complexity: O(N)
- First loop runs K times
- Second loop runs (N - K) times

Space Complexity: O(1)
```

---

### 💻 Code

```java id="cnaax5"
public double optimalApproach(int[] nums, int k) {

    int sum = 0;

    // Step 1: Build first window
    for (int i = 0; i < k; i++) {
        sum += nums[i];
    }

    int maxSum = sum;

    // Step 2: Slide the window
    for (int i = k; i < nums.length; i++) {

        sum += nums[i];       // add next
        sum -= nums[i - k];   // remove previous

        maxSum = Math.max(maxSum, sum);
    }

    return (double) maxSum / k;
}
```

---

## 🔁 Sliding Window Visualization

```
Window size = k

[1,12,-5,-6] → sum = 2
   ↓ slide
[12,-5,-6,50] → sum = 51 ✅
```

---

## ⚠️ Important Notes

* No need for:

  * HashMap ❌
  * HashSet ❌
  * While loop ❌

* This is **fixed window**, not variable

---

## 🧩 Pattern Summary

| Feature     | Value           |
| ----------- | --------------- |
| Window Type | Fixed           |
| Size        | k               |
| Expand      | Add next        |
| Shrink      | Remove previous |
| Goal        | Max sum         |

---

## 🚀 Interview One-Liner

> “Since the subarray size is fixed, I use a sliding window and reuse the previous sum by adding the next element and removing the previous one, achieving O(n) time complexity.”

---

## 🎯 Final Takeaway

```text id="xtdaqr"
Fixed size k → Sliding Window  
Reuse computation → O(N)
```

---
