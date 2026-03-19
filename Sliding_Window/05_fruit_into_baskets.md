# 904. Fruit Into Baskets

## Pattern
Sliding Window (Variable Size)  
At most **2 distinct elements**

---

## Problem

You are visiting a farm that has a single row of fruit trees arranged from left to right.  
The trees are represented by an integer array `fruits` where `fruits[i]` is the type of fruit the `i`th tree produces.

You want to collect as much fruit as possible with the following rules:

- You only have **two baskets**, and each basket can hold **only one type of fruit**.
- Each basket can hold **unlimited fruits**.
- Starting from any tree, you must pick **one fruit from each tree while moving to the right**.
- The fruits must fit into your baskets.
- If a fruit cannot fit into the baskets, you must **stop**.

Return the **maximum number of fruits you can pick**.

---

## Example 1

Input  
fruits = [1,2,1]

Output  
3

Explanation  
We can pick all fruits `[1,2,1]`.

---

## Example 2

Input  
fruits = [0,1,2,2]

Output  
3

Explanation  
We can pick `[1,2,2]`.

---

## Example 3

Input  
fruits = [1,2,3,2,2]

Output  
4

Explanation  
We can pick `[2,3,2,2]`.

---

# Java Solution

```java
class Solution {
    public int totalFruit(int[] fruits) {

        // return bruteForceApproach(fruits); // TC:- O(N^2)

        return optimalApproach(fruits); // TC:- O(N)
    }

    public int bruteForceApproach(int[] fruits) {

        int maxFruit = 0;

        for (int i = 0; i < fruits.length; i++) {

            int count = 0;

            ArrayList<Integer> choosenFruit = new ArrayList<>();

            for (int j = i; j < fruits.length; j++) {

               if (choosenFruit.size() < 2 && !choosenFruit.contains(fruits[j])){
                   choosenFruit.add(fruits[j]);
               }

               if (choosenFruit.contains(fruits[j])){
                   count++;
               }
               else {
                   break;
               }
            }

            maxFruit = Math.max(maxFruit, count);
        }

        return maxFruit;
    }

    public int optimalApproach(int[] fruits) {

        int maxFruits = 0;
        int left = 0;

        HashMap<Integer,Integer> hashMap = new HashMap<>();

        for (int right = 0; right < fruits.length; right++){

            hashMap.put(fruits[right], hashMap.getOrDefault(fruits[right],0) + 1);

            while (hashMap.size() > 2) {

                hashMap.put(fruits[left], hashMap.get(fruits[left]) - 1);

                if (hashMap.get(fruits[left]) == 0) {
                    hashMap.remove(fruits[left]);
                }

                left++;
            }

            maxFruits = Math.max(maxFruits, right - left + 1);
        }

        return maxFruits;
    }
}
