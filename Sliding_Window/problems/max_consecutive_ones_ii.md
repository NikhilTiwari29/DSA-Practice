# Max Consecutive Ones II

## Problem

You are given a binary array `nums` consisting of only `0`s and `1`s.

You can flip **at most one `0`** to `1`.

Return the maximum number of consecutive `1`s possible.

---

## Examples

### Example 1
```
Input: nums = [1, 0, 1, 1, 0]
Output: 4
Explanation: Flip first 0 → [1,1,1,1,0]
```

---

# Pattern

```
Sliding Window + Longest Valid Window
```

---

# 🧪 Brute Force Approach

## Idea

- Try flipping each `0` one by one
- For each flip:
  - Count longest consecutive 1s

---

## Java Code (Brute)

```java
public int findMaxConsecutiveOnesBrute(int[] nums) {

    int n = nums.length;
    int maxLen = 0;

    for (int i = 0; i < n; i++) {

        int zeroFlipped = 0;
        int currentLen = 0;

        for (int j = i; j < n; j++) {

            if (nums[j] == 0) {
                zeroFlipped++;
            }

            if (zeroFlipped > 1) {
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

## Complexity (Brute)

- Time: `O(n^2)`
- Space: `O(1)`

---

# 🚀 Optimized Approach (Sliding Window)

## Idea

We need the **longest subarray containing at most 1 zero**.

- Use two pointers: `left` and `right`
- Count number of zeros in window
- If zeros > 1 → shrink window
- Track max length

---

## Java Code (Optimal)

```java
public int findMaxConsecutiveOnes(int[] nums) {

    int left = 0;
    int zeroCount = 0;
    int maxLen = 0;

    for (int right = 0; right < nums.length; right++) {

        if (nums[right] == 0) {
            zeroCount++;
        }

        while (zeroCount > 1) {

            if (nums[left] == 0) {
                zeroCount--;
            }

            left++;
        }

        maxLen = Math.max(maxLen, right - left + 1);
    }

    return maxLen;
}
```

---

## Complexity (Optimized)

- Time: `O(n)`
- Space: `O(1)`

---

# 🔍 Dry Run

### Input: `[1, 0, 1, 1, 0]`

```
[1] → [1,0] → [1,0,1] → [1,0,1,1] ✅
Add next 0 → invalid (2 zeros)
Shrink → [0,1,1,0] → valid
```

Max Length = `4`

---

# 🧠 Key Insight

```
Find longest subarray with at most 1 zero
```

---

# ⚠️ Mistakes to Avoid

- Not shrinking window when zero count > 1
- Using `if` instead of `while`
- Forgetting to decrement zero count

---

# 🔁 Variations

| Problem | Change |
|--------|--------|
| Flip at most K zeros | Allow `zeroCount <= k` |
| No flips allowed | Just count consecutive 1s |
| Exactly one flip | Slight modification needed |

---

# 📌 Related Problems

- Max Consecutive Ones I
- Max Consecutive Ones III
- Longest Repeating Character Replacement
