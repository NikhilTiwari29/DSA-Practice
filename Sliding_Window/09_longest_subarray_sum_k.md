# Subarray Sum Equals K

---

## 🧠 Pattern

**Prefix Sum + HashMap (Frequency Map)**

---

## 📌 Problem

Given an integer array `nums` and an integer `k`,
return the **total number of subarrays** whose sum equals `k`.

> A subarray is a **contiguous non-empty sequence**.

---

## 🔍 Examples

### Example 1

```id="ex1"
Input: nums = [1,1,1], k = 2
Output: 2
```

---

### Example 2

```id="ex2"
Input: nums = [1,2,3], k = 3
Output: 2
```

---

## 🔍 Key Insight

```text id="key1"
We need COUNT of subarrays → not length
```

---

### 💡 Core Formula

```text id="key2"
sum(i) - sum(j) = k  
→ sum(j) = sum(i) - k
```

👉 For each index:

```text id="key3"
Check how many previous prefix sums = (current sum - k)
```

---

# 🚀 Approaches

---

## 🧪 1. Brute Force

### 💡 Idea

* Generate all subarrays
* Compute sum
* Count valid ones

---

### ⏱ Complexity

```text id="bf"
Time Complexity: O(N^2)
Space Complexity: O(1)
```

---

### 💻 Code

```java id="bfcode"
public int bruteForceApproach(int[] nums, int k) {

    int count = 0;

    for (int i = 0; i < nums.length; i++) {

        int sum = 0;

        for (int j = i; j < nums.length; j++) {

            sum += nums[j];

            if (sum == k) {
                count++;
            }
        }
    }

    return count;
}
```

---

## ⚡ 2. Optimal (Prefix Sum + HashMap)

### 💡 Idea

```text id="opt1"
Maintain prefix sum and its frequency
```

```text id="opt2"
If (sum - k) exists → add its frequency
```

---

### 🧠 Why It Works

* Prefix sum stores cumulative sum till index
* HashMap tracks how many times a prefix occurred
* Multiple matches → multiple subarrays

---

### ⏱ Complexity

```text id="opt3"
Time Complexity: O(N)
Space Complexity: O(N)
```

---

### 💻 Code

```java id="optcode"
public int optimisedApproach(int[] nums, int k) {

    Map<Integer, Integer> map = new HashMap<>();

    int sum = 0;
    int count = 0;

    // Important: handles subarrays starting from index 0
    map.put(0, 1);

    for (int i = 0; i < nums.length; i++) {

        sum += nums[i];

        int prefix = sum - k;

        // If prefix exists → valid subarray(s) found
        if (map.containsKey(prefix)) {
            count += map.get(prefix);
        }

        // Store current prefix sum frequency
        map.put(sum, map.getOrDefault(sum, 0) + 1);
    }

    return count;
}
```

---

## 🔁 Prefix Sum Visualization

```id="vis"
nums = [1,1,1], k = 2

sum = 1 → need -1 ❌  
sum = 2 → need 0 ✅  
sum = 3 → need 1 ✅  

Total = 2
```

---

## ⚠️ Important Notes

* Sliding Window ❌ (fails with negatives)
* Prefix Sum works for:

  * positive numbers
  * negative numbers
  * mixed arrays

---

## 🧩 Pattern Summary

| Feature        | Value           |
| -------------- | --------------- |
| Type           | Prefix Sum      |
| Goal           | Count subarrays |
| Data Structure | HashMap         |
| Key Operation  | sum - k         |

---

## 🔥 Golden Rule

```text id="rule1"
COUNT → Prefix Sum  
LENGTH → Sliding Window
```

---

## 🚀 Interview One-Liner

> “Since we need to count subarrays and the array may contain negative numbers, I use prefix sum with a HashMap to track frequencies.”

---

## 🎯 Final Takeaway

```text id="take"
Counting subarrays → Prefix Sum  
Not Sliding Window
```

---
