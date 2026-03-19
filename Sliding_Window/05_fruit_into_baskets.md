# 904. Fruit Into Baskets

---

## 🧠 Pattern

**Sliding Window (Variable Size) + HashMap (At Most K Distinct)**

---

## 📌 Problem

You are given an integer array `fruits` where `fruits[i]` represents the type of fruit at index `i`.

You have **2 baskets**, and each basket can hold only **one type of fruit**.

Return the **maximum number of fruits** you can collect such that the subarray contains **at most 2 distinct types**.

---

## 🧾 Constraints

* `1 <= fruits.length <= 10^5`
* `0 <= fruits[i] < fruits.length`

---

## 🔍 Examples

### Example 1

```id="f1"
Input: fruits = [1,2,1]
Output: 3
Explanation: [1,2,1]
```

---

### Example 2

```id="f2"
Input: fruits = [0,1,2,2]
Output: 3
Explanation: [1,2,2]
```

---

### Example 3

```id="f3"
Input: fruits = [1,2,3,2,2]
Output: 4
Explanation: [2,3,2,2]
```

---

## 🔍 Key Insight

```text id="key1"
We need longest subarray with at most 2 distinct elements
```

👉 General form:

```text id="key2"
Longest subarray with at most K distinct elements
```

---

# 🚀 Approaches

---

## 🧪 1. Brute Force

### 💡 Idea

* Try all subarrays
* Track at most 2 fruit types

---

### ⏱ Complexity

```text id="bf"
Time Complexity: O(N^2)
Space Complexity: O(1)
```

---

### 💻 Code

```java id="bfcode"
public int bruteForceApproach(int[] fruits) {

    int maxFruit = 0;

    for (int i = 0; i < fruits.length; i++) {

        int count = 0;
        ArrayList<Integer> choosenFruit = new ArrayList<>();

        for (int j = i; j < fruits.length; j++) {

            if (choosenFruit.size() < 2 && !choosenFruit.contains(fruits[j])) {
                choosenFruit.add(fruits[j]);
            }

            if (choosenFruit.contains(fruits[j])) {
                count++;
            } else {
                break;
            }
        }

        maxFruit = Math.max(maxFruit, count);
    }

    return maxFruit;
}
```

---

## ⚡ 2. Optimal (Sliding Window)

### 💡 Idea

```text id="opt1"
Expand → allow fruits  
Shrink → when distinct > 2  
Track max length
```

---

### 🧠 Why It Works

* We maintain a window with **≤ 2 distinct fruits**
* Use HashMap to track **frequency of fruits**

---

### ⏱ Complexity

```text id="opt2"
Time Complexity: O(N)
- right pointer moves N times
- left pointer moves N times overall

Space Complexity: O(1)
- at most 2 elements in map
```

---

### 💻 Code

```java id="optcode"
public int optimalApproach(int[] fruits) {

    int maxFruits = 0;
    int left = 0;

    HashMap<Integer, Integer> map = new HashMap<>();

    for (int right = 0; right < fruits.length; right++) {

        // Add current fruit
        map.put(fruits[right], map.getOrDefault(fruits[right], 0) + 1);

        // Shrink window if more than 2 distinct fruits
        while (map.size() > 2) {

            map.put(fruits[left], map.get(fruits[left]) - 1);

            if (map.get(fruits[left]) == 0) {
                map.remove(fruits[left]);
            }

            left++;
        }

        // Update max window size
        maxFruits = Math.max(maxFruits, right - left + 1);
    }

    return maxFruits;
}
```

---

## 🔁 Sliding Window Visualization

```id="vis"
[1,2,3,2,2]

→ [1,2,3] ❌ (3 types)  
→ shrink → [2,3]  
→ expand → [2,3,2,2] ✅ (max = 4)
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

> “This is a longest subarray problem with at most 2 distinct elements, so I use a sliding window with a HashMap to track frequencies and shrink when the constraint is violated.”

---

## 🎯 Final Takeaway

```text id="take"
At most K distinct → Sliding Window + HashMap
```

---
