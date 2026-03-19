# Longest Substring with At Most Two Distinct Characters

---

## 🧠 Pattern

**Sliding Window (Variable Size) + HashMap (At Most K Distinct)**

---

## 📌 Problem

You are given a string `s`.

Find the length of the **longest substring** that contains **at most 2 distinct characters**.

> A substring must be **contiguous**.

---

## 🔍 Examples

### Example 1

```id="ex1"
Input: s = "eceba"
Output: 3
Explanation: "ece"
```

---

### Example 2

```id="ex2"
Input: s = "ccaabbb"
Output: 5
Explanation: "aabbb"
```

---

## 🔍 Key Insight

```text id="key1"
We need longest substring with at most 2 distinct characters
```

👉 General form:

```text id="key2"
Longest substring with at most K distinct characters
```

---

# 🚀 Approaches

---

## 🧪 1. Brute Force

### 💡 Idea

* Generate all substrings
* Track distinct characters using HashSet
* Stop when distinct > 2

---

### ⏱ Complexity

```text id="bf"
Time Complexity: O(N^2)
Space Complexity: O(1)
```

---

### 💻 Code

```java id="bfcode"
public int bruteForceApproach(String s) {

    int maxLength = 0;

    for (int i = 0; i < s.length(); i++) {

        HashSet<Character> set = new HashSet<>();

        for (int j = i; j < s.length(); j++) {

            set.add(s.charAt(j));

            // If more than 2 distinct → invalid
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

## ⚡ 2. Optimal (Sliding Window)

### 💡 Idea

```text id="opt1"
Expand → add characters  
Shrink → when distinct > 2  
Track max length
```

---

### 🧠 Why It Works

* Maintain a window with **≤ 2 distinct characters**
* Use HashMap to track **frequency**

---

### ⏱ Complexity

```text id="opt2"
Time Complexity: O(N)
- Each character is added and removed at most once

Space Complexity: O(1)
- At most 2 characters in map
```

---

### 💻 Code

```java id="optcode"
public int optimalApproach(String s) {

    int maxLength = 0;
    int left = 0;

    HashMap<Character, Integer> map = new HashMap<>();

    for (int right = 0; right < s.length(); right++) {

        char ch = s.charAt(right);

        // Add current character
        map.put(ch, map.getOrDefault(ch, 0) + 1);

        // Shrink window if more than 2 distinct characters
        while (map.size() > 2) {

            char leftChar = s.charAt(left);
            map.put(leftChar, map.get(leftChar) - 1);

            if (map.get(leftChar) == 0) {
                map.remove(leftChar);
            }

            left++;
        }

        // Update max length
        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
```

---

## 🔁 Sliding Window Visualization

```id="vis"
"eceba"

e → ec → ece ✅  
eceb ❌ → shrink → ceb  
```

---

## ⚠️ Important Notes

* This is a **MAX problem**
* So:

```text id="rule1"
Shrink when INVALID (distinct > 2)
```

---

## 🧩 Pattern Summary

| Feature        | Value              |
| -------------- | ------------------ |
| Window Type    | Variable           |
| Constraint     | At most 2 distinct |
| Data Structure | HashMap            |
| Expand         | Always             |
| Shrink         | While invalid      |
| Goal           | Max length         |

---

## 🔥 Golden Rule

```text id="rule2"
"At most K" → Sliding Window + shrink when INVALID
```

---

## 🚀 Interview One-Liner

> “This is a longest substring problem with at most 2 distinct characters, so I use a sliding window with a HashMap and shrink the window when the constraint is violated.”

---

## 🎯 Final Takeaway

```text id="take"
At most K distinct → Sliding Window + HashMap
```

---
