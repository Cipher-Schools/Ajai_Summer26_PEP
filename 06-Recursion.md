# 🔁 07 — Recursion

> 🪞 **Explain Like I'm 5:** Stand between two mirrors facing each other. You see yourself, inside a smaller you, inside a smaller you… forever. Each reflection is the *same picture, just smaller.* That's recursion — **a function that calls a smaller copy of itself.**
>
> But mirrors going on forever never finish. So recursion needs a **wall to stop at.** That stopping point is called the **base case.**

> 💛 Recursion feels scary on day one for *everybody*. By the end of this file it'll feel natural. Go slow, dry-run on paper, and trust the process.

---

## The 3 Ingredients (Every Recursion Has These)

> Miss any one of these and your function calls itself forever → **StackOverflowError** (the computer runs out of memory).

1. **Base case** — the condition that *stops* the recursion (the wall).
2. **Recursive call** — the function calls itself on a **smaller** input.
3. **Progress** — each call must move *closer* to the base case (the input shrinks).

---

## The Big Idea: "Down vs Up" (Read This Twice)

This single idea explains *everything* about recursion:

> 🪜 Think of a staircase. You walk **DOWN** to the ground floor, then walk **UP** doing work.
>
> - Work written **before** the recursive call → happens on the way **DOWN** (top-to-bottom order).
> - Work written **after** the recursive call → happens on the way **UP** (bottom-to-top order).
>
> **The recursive call is the dividing line.** That's the whole secret.

---

## The Leap of Faith (The Real Skill)

> Don't try to trace the whole thing in your head. **Assume the smaller call already returns the correct answer**, then just decide what to do with it.
>
> Example: `factorial(n) = n × (whatever factorial(n-1) gives me)`.
> You don't recompute `factorial(n-1)` in your head — you *trust* it. That trust is the skill.

---

## Example 1 — Print N to 1 (work on the way DOWN)

> "I'll print `3`, then ask a smaller version of myself to print everything from `2` down. I do one line, delegate the rest."

<details>
<summary>☕ Java</summary>

```java
public static void printNto1(int n) {
    if (n == 0) {                 // base case — stop here
        return;
    }
    System.out.println(n);        // do MY one line of work...
    printNto1(n - 1);             // ...then delegate the smaller problem
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def print_n_to_1(n):
    if n == 0:                    # base case — stop here
        return
    print(n)                      # do MY one line of work...
    print_n_to_1(n - 1)           # ...then delegate the smaller problem
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
void printNto1(int n) {
    if (n == 0) {                 // base case — stop here
        return;
    }
    cout << n << endl;            // do MY one line of work...
    printNto1(n - 1);             // ...then delegate the smaller problem
}
```
</details>

**Dry run — `printNto1(3)`:**

| Call | What it does | Then calls |
|------|--------------|-----------|
| printNto1(3) | prints **3** | printNto1(2) |
| printNto1(2) | prints **2** | printNto1(1) |
| printNto1(1) | prints **1** | printNto1(0) |
| printNto1(0) | base case | returns |

**Output:** `3 2 1` — each printed on the way **down**, *before* the smaller call ran.

> ⏱️ **Time:** O(n) · **Space:** O(n) — `n` calls are stacked up waiting at once.

---

## Example 2 — The "Aha" Twist: Print 1 to N (work on the way UP)

> Same four lines. Just move the print to **after** the recursive call. Now it prints on the way **up**, and the output flips!

<details>
<summary>☕ Java</summary>

```java
public static void print1toN(int n) {
    if (n == 0) {
        return;
    }
    print1toN(n - 1);             // go ALL the way down first...
    System.out.println(n);        // ...print on the way back UP
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def print_1_to_n(n):
    if n == 0:
        return
    print_1_to_n(n - 1)           # go ALL the way down first...
    print(n)                      # ...print on the way back UP
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
void print1toN(int n) {
    if (n == 0) {
        return;
    }
    print1toN(n - 1);             // go ALL the way down first...
    cout << n << endl;            // ...print on the way back UP
}
```
</details>

**Output:** `1 2 3` — same code, *one line moved*, opposite result.

> ⭐ **The line to remember forever:** Work *before* the call → way **down**. Work *after* the call → way **up**.

---

## Example 3 — Fibonacci (when a function calls itself TWICE)

> Each Fibonacci number is the sum of the two before it: `0, 1, 1, 2, 3, 5, 8…`
> So `fib(n) = fib(n-1) + fib(n-2)` — **two** recursive calls. This makes a **tree**, not a straight line.

<details>
<summary>☕ Java</summary>

```java
public static int fib(int n) {
    if (n == 0 || n == 1) {       // two base cases (two seeds)
        return n;
    }
    return fib(n - 1) + fib(n - 2);   // TWO calls → branching
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def fib(n):
    if n == 0 or n == 1:          # two base cases (two seeds)
        return n
    return fib(n - 1) + fib(n - 2)    # TWO calls → branching
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int fib(int n) {
    if (n == 0 || n == 1) {       // two base cases (two seeds)
        return n;
    }
    return fib(n - 1) + fib(n - 2);   // TWO calls → branching
}
```
</details>

**The recursion tree for `fib(4)`:**
```
fib(4)
├── fib(3)
│   ├── fib(2)
│   │   ├── fib(1) = 1
│   │   └── fib(0) = 0
│   └── fib(1) = 1
└── fib(2)            ← computed a SECOND time! (wasted work)
    ├── fib(1) = 1
    └── fib(0) = 0
```

> ⏱️ **Time:** O(2ⁿ) — the tree roughly **doubles** each level. `fib(40)` is painfully slow! · **Space:** O(n) — only one path from root to leaf sits on the stack at once.
>
> 🔮 **This slowness gets fixed later** by *remembering* answers we already computed — that's **memoization → Dynamic Programming**. For now, just *see* the repeated work.

---

## 🪜 The Golden Rule — How To Dry-Run ANY Recursion

> 1. **Write the calls going DOWN** — peel the problem apart until the input can't shrink anymore.
> 2. **Stop at the base case** — that's your turning point, the ground floor.
> 3. **Walk back UP** — resolve each waiting line using the value returned from below.

Staircase, every time: **down to the ground floor, then back up doing the work you postponed.**

---

# 🎯 Practice — The 8 That Cover ~80% of Interviews

> Master these 8 and you'll recognise most recursion in placement interviews. Everything harder is just these combined. **Worked solutions below** — but *try each yourself first*, then check.

| # | Problem | Type | Practice Link |
|---|---------|------|---------------|
| 1 | Print 1 to N | linear (up) | https://www.geeksforgeeks.org/problems/print-1-to-n-without-using-loops-1587115620/1 |
| 2 | Factorial | linear (return) | https://www.geeksforgeeks.org/problems/factorial5739/1 |
| 3 | Sum of first N | linear (return) | https://www.geeksforgeeks.org/problems/sum-of-first-n-terms5843/1 |
| 4 | Power(x, n) | linear (return) | https://leetcode.com/problems/powx-n/ |
| 5 | Fibonacci Number | tree | https://leetcode.com/problems/fibonacci-number/ |
| 6 | Reverse a String | linear (string) | https://leetcode.com/problems/reverse-string/ |
| 7 | Valid Palindrome | two-pointer | https://leetcode.com/problems/valid-palindrome/ |
| 8 | Binary Search (recursive) | divide & conquer | https://leetcode.com/problems/binary-search/ |

---

## ✅ Solution 1 — Print 1 to N

(Full explanation above in Example 2.) The trick is printing **after** the call.

<details>
<summary>☕ Java</summary>

```java
public static void print1toN(int n) {
    if (n == 0) return;
    print1toN(n - 1);
    System.out.println(n);
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def print_1_to_n(n):
    if n == 0:
        return
    print_1_to_n(n - 1)
    print(n)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
void print1toN(int n) {
    if (n == 0) return;
    print1toN(n - 1);
    cout << n << endl;
}
```
</details>

> ⏱️ Time O(n) · Space O(n)

---

## ✅ Solution 2 — Factorial

> `n! = n × (n-1)!`. Base case `n <= 1` returns 1. **(Use `<= 1`, not `== 1`, so `factorial(0)` doesn't loop forever!)**

<details>
<summary>☕ Java</summary>

```java
public static int factorial(int n) {
    if (n <= 1) return 1;                 // safe base case
    return n * factorial(n - 1);          // trust smaller call, then multiply
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
```
</details>

**Dry run — `factorial(4)`:**

| Down (break apart) | Up (resolve) |
|--------------------|--------------|
| factorial(4) = 4 × factorial(3) | = 4 × 6 = **24** |
| factorial(3) = 3 × factorial(2) | = 3 × 2 = 6 |
| factorial(2) = 2 × factorial(1) | = 2 × 1 = 2 |
| factorial(1) = 1 (base case) | returns 1 |

> ⏱️ Time O(n) · Space O(n)

---

## ✅ Solution 3 — Sum of First N

> **Exact same skeleton as factorial — just swap `×` for `+`.** Once you see this, you've stopped memorising and started *recognising structure*.

<details>
<summary>☕ Java</summary>

```java
public static int sum(int n) {
    if (n == 0) return 0;
    return n + sum(n - 1);                // same shape, + instead of ×
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def sum_to_n(n):
    if n == 0:
        return 0
    return n + sum_to_n(n - 1)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int sum(int n) {
    if (n == 0) return 0;
    return n + sum(n - 1);
}
```
</details>

**Dry run — `sum(4)`:** 4 + 3 + 2 + 1 = **10**

> ⏱️ Time O(n) · Space O(n)

---

## ✅ Solution 4 — Power(x, n)

> `x^n = x × x^(n-1)`. Base case: anything to the power 0 is 1.
> *(Below is the simple O(n) version — perfect for learning. A faster O(log n) "fast power" exists, but understand this first.)*

<details>
<summary>☕ Java</summary>

```java
public static double power(double x, int n) {
    if (n == 0) return 1;                 // base case: x^0 = 1
    if (n < 0) return 1 / power(x, -n);   // handle negative powers
    return x * power(x, n - 1);
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def power(x, n):
    if n == 0:
        return 1                          # base case: x^0 = 1
    if n < 0:
        return 1 / power(x, -n)           # handle negative powers
    return x * power(x, n - 1)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
double power(double x, int n) {
    if (n == 0) return 1;                 // base case: x^0 = 1
    if (n < 0) return 1 / power(x, -n);   // handle negative powers
    return x * power(x, n - 1);
}
```
</details>

**Dry run — `power(2, 3)`:** 2 × 2 × 2 × 1 = **8**

> ⏱️ Time O(n) · Space O(n)

---

## ✅ Solution 5 — Fibonacci Number

(Full tree explanation above in Example 3.)

<details>
<summary>☕ Java</summary>

```java
public static int fib(int n) {
    if (n == 0 || n == 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def fib(n):
    if n == 0 or n == 1:
        return n
    return fib(n - 1) + fib(n - 2)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int fib(int n) {
    if (n == 0 || n == 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```
</details>

> ⏱️ Time O(2ⁿ) · Space O(n) — remember the repeated-work tree!

---

## ✅ Solution 6 — Reverse a String

> **Idea:** Chip off the first character, recurse on the rest, then stick that first char at the **end**. Pure leap of faith — trust `reverse` to handle the middle.

<details>
<summary>☕ Java</summary>

```java
public static String reverse(String s) {
    if (s.length() <= 1) return s;                // base: empty or 1 char
    return reverse(s.substring(1)) + s.charAt(0); // first char goes to the END
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def reverse(s):
    if len(s) <= 1:
        return s
    return reverse(s[1:]) + s[0]                   # first char goes to the END
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
string reverse(string s) {
    if (s.size() <= 1) return s;
    return reverse(s.substr(1)) + s[0];           // first char goes to the END
}
```
</details>

**Dry run — `reverse("abc")`:** `reverse("bc") + 'a'` → `reverse("c")+'b' + 'a'` → `"c" + "b" + "a"` = **"cba"**

> ⏱️ Time O(n) · Space O(n)

> 💡 The LeetCode version gives you a `char[]` and wants it reversed in-place — there you'd use the **two-pointer** method from the Two-Pointers file. This recursive version is to *understand* the idea.

---

## ✅ Solution 7 — Valid Palindrome (recursive, two-pointer)

> **Idea:** Compare the two ends. If they match, ask: "is the *inside* also a palindrome?" Base case: pointers cross (`left >= right`) → yes.

<details>
<summary>☕ Java</summary>

```java
public static boolean isPalindrome(String s, int left, int right) {
    if (left >= right) return true;               // base: pointers crossed
    if (s.charAt(left) != s.charAt(right)) return false;
    return isPalindrome(s, left + 1, right - 1);  // check the inside
}
// call it as: isPalindrome(s, 0, s.length() - 1);
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def is_palindrome(s, left, right):
    if left >= right:
        return True                               # base: pointers crossed
    if s[left] != s[right]:
        return False
    return is_palindrome(s, left + 1, right - 1)  # check the inside
# call it as: is_palindrome(s, 0, len(s) - 1)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
bool isPalindrome(string s, int left, int right) {
    if (left >= right) return true;               // base: pointers crossed
    if (s[left] != s[right]) return false;
    return isPalindrome(s, left + 1, right - 1);  // check the inside
}
// call it as: isPalindrome(s, 0, s.size() - 1);
```
</details>

> ⏱️ Time O(n) · Space O(n)

---

## ✅ Solution 8 — Binary Search (recursive)

> **Divide and conquer IS recursion.** Look at the middle. Too big? Recurse on the left half. Too small? Recurse on the right half. Base case: range is empty (`low > high`) → not found.

<details>
<summary>☕ Java</summary>

```java
public static int binarySearch(int[] arr, int low, int high, int target) {
    if (low > high) return -1;                    // base: empty range
    int mid = low + (high - low) / 2;
    if (arr[mid] == target) return mid;
    if (arr[mid] < target)
        return binarySearch(arr, mid + 1, high, target);   // right half
    else
        return binarySearch(arr, low, mid - 1, target);    // left half
}
// call it as: binarySearch(arr, 0, arr.length - 1, target);
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def binary_search(arr, low, high, target):
    if low > high:
        return -1                                 # base: empty range
    mid = (low + high) // 2
    if arr[mid] == target:
        return mid
    if arr[mid] < target:
        return binary_search(arr, mid + 1, high, target)   # right half
    else:
        return binary_search(arr, low, mid - 1, target)    # left half
# call it as: binary_search(arr, 0, len(arr) - 1, target)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int binarySearch(int arr[], int low, int high, int target) {
    if (low > high) return -1;                    // base: empty range
    int mid = low + (high - low) / 2;
    if (arr[mid] == target) return mid;
    if (arr[mid] < target)
        return binarySearch(arr, mid + 1, high, target);   // right half
    else
        return binarySearch(arr, low, mid - 1, target);    // left half
}
// call it as: binarySearch(arr, 0, n - 1, target);
```
</details>

> ⏱️ Time O(log n) · Space O(log n) — the stack is only as deep as the number of halvings.

---

## 📋 One-Glance Reference

| Type | # calls | Time | Space | Examples |
|------|---------|------|-------|----------|
| **Linear (work down)** | 1, before call | O(n) | O(n) | printNto1 |
| **Linear (work up / return)** | 1, after call | O(n) | O(n) | print1toN, factorial, sum, power |
| **Tree (branching)** | 2+ | O(2ⁿ) | O(n) | fibonacci |
| **Divide & conquer** | 1 of 2 halves | O(log n) | O(log n) | binary search |

---

## ❓ Common Doubts (Quick Answers)

- **What is StackOverflowError?** The call stack has a finite size. A missing/unreachable base case → infinite calls → stack fills up → crash. It's the computer saying "you never stopped."
- **Why is recursion sometimes slower than a loop?** Function calls aren't free (each makes a stack frame), and tree recursion like `fib` redoes the same subproblems. A loop reuses one frame and never recomputes.
- **When should I use recursion?** When the problem is naturally self-similar — trees, divide & conquer, backtracking. For a flat count up/down, a loop is usually cleaner.

---

> 🌟 **You did it.** Recursion is the gateway to trees, backtracking, and dynamic programming — the "scary" topics that are just *recursion with a memory*. Get these 8 solid, dry-run them on paper, and you're ahead of most beginners. I'm right here for any doubt. 💪 — *Ajai Raj (Mentor)*
