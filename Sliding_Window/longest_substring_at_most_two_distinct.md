# Longest Substring with At Most Two Distinct Characters

## Problem

You are given a string `s`.  
Find the length of the **longest substring** that contains **at most 2 distinct characters**.

---

## Examples

### Example 1
```
Input: s = "eceba"
Output: 3
Explanation: "ece"
```

### Example 2
```
Input: s = "ccaabbb"
Output: 5
Explanation: "aabbb"
```

---

# Pattern

```
Sliding Window + K Distinct Elements
```

---

# 🧪 Brute Force Approach

## Idea

- Generate all substrings
- For each substring:
  - Count distinct characters
  - If ≤ 2 → update answer

---

## Java Code (Brute Force)

```java
public int lengthOfLongestSubstringTwoDistinctBrute(String s) {

    int n = s.length();
    int maxLength = 0;

    for (int i = 0; i < n; i++) {

        HashSet<Character> set = new HashSet<>();

        for (int j = i; j < n; j++) {

            set.add(s.charAt(j));

            if (set.size() > 2) {
                break;
            }

            maxLength = Math.max(maxLength, j - i + 1);
        }
    }

    return maxLength;
}
```

---

## Complexity (Brute)

- Time: `O(n^2)`
- Space: `O(1)` (at most 3 characters)

---

# 🚀 Optimized Approach (Sliding Window)

## Idea

- Use two pointers: `left` and `right`
- Maintain a `HashMap` for frequency
- Expand window
- If distinct > 2 → shrink window
- Track max length

---

## Java Code (Optimal)

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

## Complexity (Optimized)

- Time: `O(n)`
- Space: `O(1)`

---

# 🔍 Dry Run

### Input: `"eceba"`

```
e → ec → ece ✅
eceb ❌ → shrink → eb
```

Answer = `3`

---

### Input: `"ccaabbb"`

```
cc → ccaa → ccaab ❌
shrink → aabbb ✅
```

Answer = `5`

---

# 🧠 Key Insight

```
Control the number of distinct characters in the window
```

---

# ⚠️ Mistakes to Avoid

- Using `if` instead of `while` for shrinking
- Not removing characters when frequency becomes 0
- Updating answer when window is invalid

---

# 🔁 Variations

| Problem | Approach |
|--------|--------|
| At most K distinct | Same template, replace `2` with `k` |
| Exactly K distinct | atMost(k) - atMost(k-1) |
| No duplicates | Use HashSet instead of HashMap |

---

# 📌 Related Problems

- Longest Substring Without Repeating Characters
- Fruit Into Baskets
- Longest Repeating Character Replacement
