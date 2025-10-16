# LEETCODE-Arrays-2598
---

### 💡 Code Purpose

This code finds the **smallest non-negative integer (MEX)** that **cannot** be formed from the given array `nums`, if we can repeatedly add or subtract the given `value` to/from each number.

---

### 🧩 Example Input

```java
nums = [1, 2, 3, 4, 5]
value = 2
```

---

### 🔍 Step 1: Initialize HashMap

```java
HashMap<Integer,Integer> hash = new HashMap<>();
```

→ `hash` will store counts of remainders when each number is divided by `value`.

---

### 🔁 Step 2: Build HashMap

For each `num` in `nums`:

Formula used:

```java
r = ((num % value) + value) % value
```

This ensures remainder `r` is always **non-negative** (important for negative numbers).

| num | num % value | ((num % value)+value)%value | hash after update |
| --- | ----------- | --------------------------- | ----------------- |
| 1   | 1           | 1                           | {1=1}             |
| 2   | 0           | 0                           | {1=1, 0=1}        |
| 3   | 1           | 1                           | {1=2, 0=1}        |
| 4   | 0           | 0                           | {1=2, 0=2}        |
| 5   | 1           | 1                           | {1=3, 0=2}        |

✅ After loop:

```java
hash = {0=2, 1=3}
```

---

### 🔁 Step 3: Find MEX

Initialize:

```java
MEX = 0
```

Now loop while:

```java
hash.getOrDefault(MEX % value, 0) > 0
```

Let’s go step-by-step:

| MEX | MEX % value | hash.getOrDefault(...) | Action                                     |
| --- | ----------- | ---------------------- | ------------------------------------------ |
| 0   | 0           | 2                      | >0 → reduce count of 0 → {0=1, 1=3}, MEX=1 |
| 1   | 1           | 3                      | >0 → reduce count of 1 → {0=1, 1=2}, MEX=2 |
| 2   | 0           | 1                      | >0 → reduce count of 0 → {0=0, 1=2}, MEX=3 |
| 3   | 1           | 2                      | >0 → reduce count of 1 → {0=0, 1=1}, MEX=4 |
| 4   | 0           | 0                      | ==0 → stop loop                            |

---

### ✅ Step 4: Return Answer

MEX = **4**

---

### 🧠 Summary of Logic

* Each number contributes to a *remainder class* (`num % value`).
* You can generate numbers of that remainder type by adding/subtracting multiples of `value`.
* You reduce the available counts until one remainder class can’t generate the next integer.
* The loop breaks at the first integer that can’t be formed → that’s the **MEX**.

---

### ✅ Final Output for the Example

```
Output = 4
```

---
