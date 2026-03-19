# Longest Subarray with Sum K

## Problem

Given an array `arr[]` of integers and an integer `k`,  
find the **length of the longest subarray** whose sum equals `k`.

---

## Examples

### Example 1
```
Input: arr = [1, 2, 3, 1, 1, 1], k = 3
Output: 3
Explanation: Subarray [1,1,1]
```

---

### Example 2
```
Input: arr = [1, 2, 3, 4, 5], k = 9
Output: 3
Explanation: Subarray [2,3,4]
```

---

# Pattern

```
Prefix Sum + HashMap
```

---

# 🧪 Brute Force Approach

## Idea

- Generate all subarrays
- Calculate sum for each
- If sum == k → update max length

---

## Java Code (Brute)

```java
public int longestSubarrayBrute(int[] arr, int k) {

    int maxLength = 0;

    for (int i = 0; i < arr.length; i++) {

        int sum = 0;

        for (int j = i; j < arr.length; j++) {

            sum += arr[j];

            if (sum == k) {
                maxLength = Math.max(maxLength, j - i + 1);
            }
        }
    }

    return maxLength;
}
```

---

## Complexity (Brute)

- Time: `O(n^2)`
- Space: `O(1)`

---

# ⚡ Better Approach (Prefix Sum + HashMap)

## Idea

- Maintain prefix sum
- If `(sum - k)` exists → subarray found
- Store first occurrence of each prefix sum

---

## Java Code (Better)

```java
public int longestSubarrayBetter(int[] arr, int k) {

    HashMap<Integer, Integer> map = new HashMap<>();

    int sum = 0;
    int maxLength = 0;

    for (int i = 0; i < arr.length; i++) {

        sum += arr[i];

        if (sum == k) {
            maxLength = Math.max(maxLength, i + 1);
        }

        if (map.containsKey(sum - k)) {
            maxLength = Math.max(maxLength, i - map.get(sum - k));
        }

        // store only first occurrence
        if (!map.containsKey(sum)) {
            map.put(sum, i);
        }
    }

    return maxLength;
}
```

---

## Complexity (Better)

- Time: `O(n)`
- Space: `O(n)`

---

# 🚀 Optimal Approach (Sliding Window)

## ⚠️ Important Condition

```
Works ONLY when array contains NON-NEGATIVE numbers (positives and zero)
```

---

## ❓ Why this condition is required

Sliding window depends on **monotonic behavior of sum**:

- Adding elements → sum increases
- Removing elements → sum decreases

This property holds only for **non-negative numbers**.

---

## ❌ Why it fails for negative numbers

Example:

```
arr = [2, -1, 2], k = 3
```

- Expanding window may decrease sum
- Shrinking window may increase sum

➡️ Window becomes unpredictable  
➡️ Sliding window fails

---

## ✅ When to Use Sliding Window

| Array Type | Can Use Sliding Window? |
|-----------|------------------------|
| All positive | ✅ Yes |
| Positive + zero | ✅ Yes |
| Contains negatives | ❌ No |

---

## Idea

- Use two pointers (`i`, `j`)
- Expand window
- If sum > k → shrink window
- Track max length

---

## Java Code (Optimal)

```java
public int longestSubarrayOptimal(int[] arr, int k) {

    int i = 0;
    int sum = 0;
    int maxLength = 0;

    for (int j = 0; j < arr.length; j++) {

        sum += arr[j];

        while (sum > k && i <= j) {
            sum -= arr[i];
            i++;
        }

        if (sum == k) {
            maxLength = Math.max(maxLength, j - i + 1);
        }
    }

    return maxLength;
}
```

---

## Complexity (Optimal)

- Time: `O(n)`
- Space: `O(1)`

---

# 🔍 Dry Run

### Input: `[1, 2, 3, 1, 1, 1], k = 3`

```
[1,2] → sum = 3 ✅
[3] → sum = 3 ✅
[1,1,1] → sum = 3 ✅ (max = 3)
```

---

# 🧠 Key Insight

```
If negatives exist → use Prefix Sum + HashMap
If only non-negative → use Sliding Window
```

---

# ⚠️ Mistakes to Avoid

- Using sliding window when negatives exist ❌
- Not storing first occurrence of prefix sum ❌
- Updating map incorrectly ❌

---

# 🔁 Variations

| Problem | Approach |
|--------|--------|
| Count subarrays with sum k | Prefix sum frequency |
| Longest subarray with sum ≤ k | Sliding window |
| Binary array (0/1) | Sliding window works |

---

# 📌 Related Problems

- Subarray Sum Equals K
- Longest Subarray with Sum ≤ K
- Maximum Size Subarray Sum Equals K
