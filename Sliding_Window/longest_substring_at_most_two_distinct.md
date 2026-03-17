# Longest Substring with At Most Two Distinct Characters

## Problem

You are given a string `s`.  
Find the length of the **longest substring** that contains **at most 2 distinct characters**.

A substring is a contiguous sequence of characters.

---

## Examples

### Example 1

```
Input: s = "eceba"
Output: 3
Explanation: "ece"
```

---

### Example 2

```
Input: s = "ccaabbb"
Output: 5
Explanation: "aabbb"
```

---

## Pattern

```
Sliding Window + K Distinct Elements
```

---

## How to Identify

| Clue in Problem | Pattern |
|----------------|--------|
| "at most 2 distinct" | Sliding Window with K Distinct |

---

## Approach

- Use a sliding window `[left, right]`
- Maintain a `HashMap` to track frequency of characters
- Expand the window using `right`
- If distinct characters exceed 2 → shrink from `left`
- Keep updating maximum length

---

## Algorithm

1. Initialize:
   - `left = 0`
   - `maxLength = 0`
   - `HashMap<Character, Integer> map`

2. Traverse using `right` pointer:
   - Add current character to map
   - If map size > 2:
     - Shrink window from left
     - Decrease frequency
     - Remove character if frequency becomes 0

3. Update answer:
   ```
   maxLength = max(maxLength, right - left + 1)
   ```

---

## Java Code

```java
public int lengthOfLongestSubstringTwoDistinct(String s) {

    int left = 0;
    int maxLength = 0;

    HashMap<Character, Integer> map = new HashMap<>();

    for (int right = 0; right < s.length(); right++) {

        char c = s.charAt(right);
        map.put(c, map.getOrDefault(c, 0) + 1);

        while (map.size() > 2) {

            char leftChar = s.charAt(left);
            map.put(leftChar, map.get(leftChar) - 1);

            if (map.get(leftChar) == 0) {
                map.remove(leftChar);
            }

            left++;
        }

        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
```

---

## Dry Run

### Input: `"eceba"`

```
e → ec → ece ✅
eceb ❌ (3 distinct)
Shrink → ceb → eb
```

Max Length = `3`

---

### Input: `"ccaabbb"`

```
cc → ccaa → ccaab ❌
Shrink → aabbb ✅
```

Max Length = `5`

---

## Complexity

- Time Complexity: `O(n)`
- Space Complexity: `O(1)` (at most 3 characters in map)

---

## Key Insight

```
Control the number of distinct characters in the window
```

---

## Variations

| Problem Variation | Approach |
|------------------|---------|
| At most K distinct | Replace `2` with `k` |
| Exactly K distinct | Use helper: atMost(K) - atMost(K-1) |
| Only 1 distinct | Longest repeating character |

---

## Mistakes to Avoid

- Using `if` instead of `while` for shrinking
- Forgetting to remove character when frequency becomes 0
- Updating answer before making window valid

---

## Related Problems

- Longest Substring Without Repeating Characters
- Fruit Into Baskets
- Longest Repeating Character Replacement
