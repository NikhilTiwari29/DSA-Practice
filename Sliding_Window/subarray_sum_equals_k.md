# Subarray Sum Equals K

## Problem

Given an integer array `nums` and an integer `k`,  
return the **total number of subarrays** whose sum equals `k`.

---

## Examples

### Example 1
```
Input: nums = [1,1,1], k = 2
Output: 2
Explanation: [1,1] (two times)
```

---

### Example 2
```
Input: nums = [1,2,3], k = 3
Output: 2
Explanation: [1,2], [3]
```

---

# Pattern

```
Prefix Sum + HashMap (Frequency Map)
```

---

# 🧪 Brute Force Approach

## Idea

- Generate all subarrays
- Calculate sum for each
- If sum == k → increment count

---

## Java Code (Brute)

```java
public int subarraySumBrute(int[] nums, int k) {

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

## Complexity (Brute)

- Time: `O(n^2)`
- Space: `O(1)`

---

# 🚀 Optimized Approach (Prefix Sum + HashMap)

## Idea

- Maintain prefix sum
- If `(sum - k)` exists → subarray found
- Use map to store **frequency of prefix sums**

---

## 🔥 Key Logic

```
If sum(i) - sum(j) = k
→ sum(j) = sum(i) - k
```

---

## Java Code (Optimal)

```java
public int subarraySum(int[] nums, int k) {

    Map<Integer, Integer> map = new HashMap<>();

    int sum = 0;
    int count = 0;

    map.put(0, 1); // important

    for (int i = 0; i < nums.length; i++) {

        sum += nums[i];

        int prefix = sum - k;

        if (map.containsKey(prefix)) {
            count += map.get(prefix); // important
        }

        map.put(sum, map.getOrDefault(sum, 0) + 1);
    }

    return count;
}
```

---

## ⚠️ Important Points

### 1. Why `map.put(0,1)`?

```
Handles subarrays starting from index 0
```

Example:
```
[1,2,3], k = 3
```

When sum = 3 → prefix = 0 → count++
```

---

### 2. Why `count += map.get(prefix)`?

```
Because multiple subarrays can have same prefix sum
```

---

## Complexity (Optimal)

- Time: `O(n)`
- Space: `O(n)`

---

# 🔍 Dry Run

### Input: `[1,1,1], k = 2`

```
sum = 1 → prefix = -1 → not found
map = {0:1, 1:1}

sum = 2 → prefix = 0 → count = 1
map = {0:1, 1:1, 2:1}

sum = 3 → prefix = 1 → count = 2
```

---

# 🧠 Key Insight

```
Count subarrays → use prefix sum frequency
```

---

# ❌ Why Sliding Window Fails

```
Array may contain negative numbers
→ sum is not monotonic
→ window expansion/shrinking breaks
```

---

# 🔁 Variations

| Problem | Approach |
|--------|--------|
| Count subarrays with sum k | Prefix sum + frequency |
| Longest subarray with sum k | Prefix sum + first occurrence |
| Subarray sum divisible by k | Prefix sum + modulo |

---

# ⚠️ Mistakes to Avoid

- Forgetting `map.put(0,1)` ❌
- Using `+1` instead of frequency ❌
- Trying sliding window ❌

---

# 📌 Related Problems

- Longest Subarray with Sum K
- Subarray Sum Divisible by K
- Binary Subarrays With Sum
