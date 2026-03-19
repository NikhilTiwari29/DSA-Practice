# 643. Maximum Average Subarray I

---

## 🧠 Pattern

**Sliding Window (Fixed Size)**

---

## 📌 Problem

You are given an integer array `nums` and an integer `k`.

Find a **contiguous subarray of size k** that has the **maximum average value**.

---

## 🔍 Key Insight

```text id="xtxiqo"
Since k is FIXED → maximizing average = maximizing sum
```

👉 So we only need to track **maximum sum of size k window**

---

## 🚀 Approaches

---

# 🧪 1. Brute Force

### 💡 Idea

* Try every subarray of size `k`
* Compute sum each time

---

### ⏱ Complexity

```text id="a8yd8k"
Time Complexity: O(N * K)
- Outer loop runs N times
- Inner loop runs K times (building each window)

Space Complexity: O(1)
- No extra space used
```

---

### 💻 Code

```java id="tpmkoi"
public double bruteForceApproach(int[] nums, int k) {

    double maxAverage = Double.NEGATIVE_INFINITY;

    // Try every starting index
    for (int i = 0; i < nums.length; i++) {

        int sum = 0;
        int count = 0;

        // Build subarray of size k
        for (int j = i; j < nums.length; j++) {

            sum += nums[j];
            count++;

            // Once size becomes k → calculate average
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

# ⚡ 2. Optimal (Sliding Window)

### 💡 Idea

Instead of recomputing sum:

```text id="fkjdus"
Reuse previous window sum
```

```text id="zvyqei"
New window = old window + next element - previous element
```

---

### 🧠 Why It Works

* Window size is **fixed (k)**
* Each step does **constant work**

---

### ⏱ Complexity

```text id="8qk0k7"
Time Complexity: O(N)
- First loop runs K times
- Second loop runs (N - K) times
- Total = O(N)

Space Complexity: O(1)
- Only variables used (sum, maxSum)
```

---

### 💻 Code

```java id="cnaax5"
public double optimalApproach(int[] nums, int k) {

    int sum = 0;

    // Step 1: Build first window [0 ... k-1]
    for (int i = 0; i < k; i++) {
        sum += nums[i];
    }

    int maxSum = sum;

    // Step 2: Slide the window
    for (int i = k; i < nums.length; i++) {

        sum += nums[i];       // add next element
        sum -= nums[i - k];   // remove element going out

        maxSum = Math.max(maxSum, sum);
    }

    return (double) maxSum / k;
}
```

---

# 🔁 Sliding Window Visualization

```id="6vxpa7"
Window size = k

[1,12,-5,-6] → sum = 2
   ↓ slide
[12,-5,-6,50] → sum = 51 ✅
```

---

# ⚠️ Important Notes

* No need for:

  * HashMap ❌
  * HashSet ❌
  * While loop ❌

* This is **fixed window**, not variable

---

# 🧩 Pattern Summary

| Feature     | Value           |
| ----------- | --------------- |
| Window Type | Fixed           |
| Size        | k               |
| Expand      | Add next        |
| Shrink      | Remove previous |
| Goal        | Max sum         |

---

# 🚀 Interview One-Liner

> “Since the subarray size is fixed, I use a sliding window where I reuse the previous sum by adding the next element and removing the previous one, achieving O(n) time complexity.”

---

# 🎯 Final Takeaway

```text id="xtdaqr"
Fixed size k → Sliding Window  
Reuse computation → O(N)
```

---
