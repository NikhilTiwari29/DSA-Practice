# 3. Longest Substring Without Repeating Characters

---

## 🧠 Pattern

**Sliding Window (Variable Size) + HashSet**

---

## 📌 Problem

Given a string `s`, find the length of the **longest substring** without repeating characters.

> ⚠️ A substring must be **contiguous**.

---

## 🧾 Constraints

* `0 <= s.length <= 5 * 10^4`
* `s` consists of English letters, digits, symbols, and spaces

---

## 🔍 Examples

### Example 1

```id="n1q2w3"
Input: s = "abcabcbb"
Output: 3
Explanation: "abc"
```

---

### Example 2

```id="n2q3w4"
Input: s = "bbbbb"
Output: 1
Explanation: "b"
```

---

### Example 3

```id="n3q4w5"
Input: s = "pwwkew"
Output: 3
Explanation: "wke"
```

---

## 🔍 Key Insight

```text id="f3p8z1"
We need longest substring with ALL UNIQUE characters
```

👉 Maintain a window with **no duplicates**

---

# 🚀 Approaches

---

## 🧪 1. Brute Force

### 💡 Idea

* Try all substrings
* Check uniqueness using HashSet

---

### ⏱ Complexity

```text id="bf1"
Time Complexity: O(N^2)
Space Complexity: O(N)
```

---

### 💻 Code

```java id="bfcode"
public int bruteForceApproach(String s) {

    int maxSize = 0;

    for (int i = 0; i < s.length(); i++) {

        HashSet<Character> set = new HashSet<>();

        for (int j = i; j < s.length(); j++) {

            char ch = s.charAt(j);

            if (!set.contains(ch)) {
                set.add(ch);
            } else {
                break;
            }

            maxSize = Math.max(maxSize, set.size());
        }
    }

    return maxSize;
}
```

---

## ⚡ 2. Optimal (Sliding Window)

### 💡 Idea

```text id="opt1"
Expand → until duplicate appears  
Shrink → until duplicate removed  
Track max length
```

---

### 🧠 Why It Works

* We maintain a **valid window (no duplicates)**
* Adjust dynamically using two pointers

---

### ⏱ Complexity

```text id="opt2"
Time Complexity: O(N)
- Each character is added and removed at most once

Space Complexity: O(N)
- HashSet stores characters
```

---

### 💻 Code

```java id="optcode"
public int optimisedApproach(String s) {

    int maxSize = 0;
    int left = 0;

    HashSet<Character> set = new HashSet<>();

    for (int right = 0; right < s.length(); right++) {

        char ch = s.charAt(right);

        // Shrink window until duplicate is removed
        while (set.contains(ch)) {
            set.remove(s.charAt(left));
            left++;
        }

        // Add current character
        set.add(ch);

        // Update max length
        maxSize = Math.max(maxSize, right - left + 1);
    }

    return maxSize;
}
```

---

## 🔁 Sliding Window Visualization

```id="vis1"
"abcabcbb"

abc → valid  
abca → duplicate → shrink → bca  
bca → valid
```

---

## ⚠️ Important Notes

* This is a **MAX problem**
* So:

```text id="rule1"
Shrink when INVALID (duplicate found)
```

---

## 🧩 Pattern Summary

| Feature        | Value         |
| -------------- | ------------- |
| Window Type    | Variable      |
| Constraint     | No duplicates |
| Data Structure | HashSet       |
| Expand         | Always        |
| Shrink         | While invalid |
| Goal           | Max length    |

---

## 🔥 Golden Rule

```text id="rule2"
MAX problem → shrink when INVALID
```

---

## 🚀 Interview One-Liner

> “I use a sliding window with a HashSet to maintain unique characters. When a duplicate appears, I shrink the window until it becomes valid again.”

---

## 🎯 Final Takeaway

```text id="take1"
Longest substring + uniqueness constraint  
→ Sliding Window + HashSet
```

---
