# Sliding Window Templates

Sliding window is a technique used to process **subarrays or substrings efficiently**.

Instead of recomputing results for every window, we **reuse information from the previous window**.

Most interview problems fall into **6 common sliding window patterns**.

---

# 1. Fixed Size Sliding Window

## When to Use
When the window size **k is fixed**.

Example problems:
- Maximum Sum Subarray of Size K
- Maximum Average Subarray

---

## Idea

Instead of recalculating the sum for every window:

```
newWindow = oldWindow
+ incomingElement
- outgoingElement
```

---

## Java Template

```java
int windowSum = 0;

// first window
for(int i = 0; i < k; i++){
    windowSum += arr[i];
}

int result = windowSum;

for(int i = k; i < arr.length; i++){

    windowSum += arr[i];      // add new element
    windowSum -= arr[i - k];  // remove old element

    result = Math.max(result, windowSum);
}
```

Time Complexity: `O(n)`

---

# 2. Variable Window (Expand + Shrink)

## When to Use

When the window size is **not fixed** and must satisfy a **condition**.

Example problems:

- Minimum Size Subarray Sum
- Smallest Subarray With Given Sum

---

## Idea

```
Expand window until condition satisfied
Then shrink from left
```

---

## Java Template

```java
int left = 0;
int sum = 0;

for(int right = 0; right < arr.length; right++){

    sum += arr[right];

    while(sum >= target){

        updateAnswer();

        sum -= arr[left];
        left++;
    }
}
```

Time Complexity: `O(n)`

---

# 3. Longest Valid Window

## When to Use

When the problem asks for:

- Longest subarray
- Maximum length substring
- Window must satisfy a rule

Example problems:

- Max Consecutive Ones III
- Longest Repeating Character Replacement

---

## Idea

```
Expand window
If window becomes invalid
    shrink window
Track maximum size
```

---

## Java Template

```java
int left = 0;
int maxLength = 0;

for(int right = 0; right < arr.length; right++){

    updateWindow();

    while(windowInvalid()){
        shrinkWindow();
        left++;
    }

    maxLength = Math.max(maxLength, right - left + 1);
}
```

Time Complexity: `O(n)`

---

# 4. Sliding Window with K Distinct Elements

## When to Use

When window must contain **at most K distinct elements**.

Example problems:

- Fruit Into Baskets
- Longest Substring with At Most K Distinct Characters

---

## Idea

Use a **HashMap** to track frequency.

Shrink window if distinct elements exceed `k`.

---

## Java Template

```java
int left = 0;

HashMap<Character,Integer> map = new HashMap<>();

for(int right = 0; right < s.length(); right++){

    char c = s.charAt(right);

    map.put(c, map.getOrDefault(c,0) + 1);

    while(map.size() > k){

        char leftChar = s.charAt(left);

        map.put(leftChar, map.get(leftChar) - 1);

        if(map.get(leftChar) == 0){
            map.remove(leftChar);
        }

        left++;
    }

    updateAnswer(right - left + 1);
}
```

Time Complexity: `O(n)`

---

# 5. Sliding Window with No Duplicates

## When to Use

When the window must contain **unique elements only**.

Example problems:

- Longest Substring Without Repeating Characters

---

## Idea

Use a **HashSet** to maintain unique characters.

If duplicate appears → shrink window.

---

## Java Template

```java
int left = 0;

HashSet<Character> set = new HashSet<>();

for(int right = 0; right < s.length(); right++){

    while(set.contains(s.charAt(right))){
        set.remove(s.charAt(left));
        left++;
    }

    set.add(s.charAt(right));

    updateAnswer(right - left + 1);
}
```

Time Complexity: `O(n)`

---

# 6. Frequency Based Sliding Window

## When to Use

When window validity depends on **character frequencies**.

Example problems:

- Permutation in String
- Find All Anagrams in a String

---

## Idea

Track frequencies using an array or map.

Check if window matches required frequency.

---

## Java Template

```java
int[] freq = new int[26];

int left = 0;

for(int right = 0; right < s.length(); right++){

    updateFrequency();

    while(windowInvalid()){
        removeLeftFrequency();
        left++;
    }

    updateAnswer();
}
```

---

# How to Identify the Pattern

| Problem Clue | Pattern |
|---|---|
| Window size `k` is given | Fixed Window |
| Condition like `sum >= target` | Expand + Shrink |
| Longest/Maximum subarray | Longest Valid Window |
| At most K distinct | K Distinct |
| No repeating characters | No Duplicates |
| Frequency comparison | Frequency Based |

---

# General Sliding Window Structure

```
expand right pointer
    update window state

while window becomes invalid
    shrink left pointer

update answer
```

---

# Common Mistakes

1. Using `if` instead of `while` when shrinking window
2. Updating answer in the wrong place
3. Forgetting to remove element when shrinking
4. Not handling edge cases

---

# Key Insight

Almost every sliding window problem follows:

```
Expand → Check condition → Shrink → Update answer
```

Mastering these patterns allows solving **most sliding window problems in O(n)**.
