# 🔤 05 — Strings

> 🪄 **The one mantra for all of strings:**
> **"A String is just an array of characters."**
> Everything you learned about arrays — two pointers, counting — works here. You already know strings. You just don't know it yet.

---

## The 2 Weapons That Solve Almost Every String Problem

1. **Two pointers** → reverse, palindrome
2. **A frequency/count array `int[26]`** → anagram, unique character

---

## The Magic `c - 'a'` Trick (Spend Real Time Here)

> 🔑 Letters have secret numbers (ASCII): `'a'` = 97, `'b'` = 98, ... `'z'` = 122.
> So:
> - `'a' - 'a'` = 0
> - `'b' - 'a'` = 1
> - `'z' - 'a'` = 25
>
> `c - 'a'` turns any lowercase letter into a number **0–25**. That lets a 26-box array act as a "letter counter." **Half of string problems depend on this one line.**

---

## Problem 1 — Check Palindrome (two pointers)

> A palindrome reads the same both ways: `madam`, `racecar`.

<details>
<summary>☕ Java</summary>

```java
boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) return false;
        left++;
        right--;
    }
    return true;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def is_palindrome(s):
    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True
    # Shortcut (learn the long way first): return s == s[::-1]
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
bool isPalindrome(string s) {
    int left = 0, right = s.size() - 1;
    while (left < right) {
        if (s[left] != s[right]) return false;
        left++;
        right--;
    }
    return true;
}
```
</details>

---

## Problem 2 — Check Anagram (frequency array)

> Two words are anagrams if they use the **same letters**: `listen` & `silent`.
> **Trick:** Count letters in word A, subtract for word B. If all counts end at 0 → they match.

<details>
<summary>☕ Java</summary>

```java
boolean isAnagram(String a, String b) {
    if (a.length() != b.length()) return false;
    int[] count = new int[26];                  // 26 boxes, one per letter
    for (int i = 0; i < a.length(); i++) {
        count[a.charAt(i) - 'a']++;             // add for word a
        count[b.charAt(i) - 'a']--;             // subtract for word b
    }
    for (int c : count) if (c != 0) return false;
    return true;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def is_anagram(a, b):
    if len(a) != len(b):
        return False
    count = [0] * 26                            # 26 boxes, one per letter
    for i in range(len(a)):
        count[ord(a[i]) - ord('a')] += 1        # add for word a
        count[ord(b[i]) - ord('a')] -= 1        # subtract for word b
    return all(c == 0 for c in count)
    # Shortcut: from collections import Counter; return Counter(a) == Counter(b)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
bool isAnagram(string a, string b) {
    if (a.size() != b.size()) return false;
    int count[26] = {0};                        // 26 boxes, one per letter
    for (int i = 0; i < a.size(); i++) {
        count[a[i] - 'a']++;                    // add for word a
        count[b[i] - 'a']--;                    // subtract for word b
    }
    for (int c : count) if (c != 0) return false;
    return true;
}
```
</details>

---

## ⚠️ Java Gotcha (Drill Once)

> In Java, `String` is **immutable** — it can't be changed after creation.
> Doing `s = s + c` inside a loop is secretly **O(n²)** (slow!).
> Use a **`char[]`** or **`StringBuilder`** instead when building strings in a loop.

---

## 🎯 Practice (Easy First)

| Problem | Where | Link |
|---------|-------|------|
| Valid Palindrome | LeetCode | https://leetcode.com/problems/valid-palindrome/ |
| Valid Anagram | LeetCode | https://leetcode.com/problems/valid-anagram/ |
| First Unique Character in a String | LeetCode | https://leetcode.com/problems/first-unique-character-in-a-string/ |
| Reverse String | LeetCode | https://leetcode.com/problems/reverse-string/ |
| Reverse Words in a String | LeetCode | https://leetcode.com/problems/reverse-words-in-a-string/ |

> 💡 **Order to attack:** Reverse String → Valid Palindrome → Valid Anagram. Each one reuses the *exact* two weapons above. Notice the pattern repeating — that's the moment strings stop feeling scary. 🌟

---

# ✅ Worked Solutions

> Try each yourself first, then check. All three languages for every problem.

## Solution 1 — Valid Palindrome

> **Problem:** Check if a string is a palindrome, considering only letters & numbers, ignoring case.
> **Weapon used:** two pointers walking inward.

<details>
<summary>☕ Java</summary>

```java
boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;
        if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right)))
            return false;
        left++; right--;
    }
    return true;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def is_palindrome(s):
    left, right = 0, len(s) - 1
    while left < right:
        while left < right and not s[left].isalnum():
            left += 1
        while left < right and not s[right].isalnum():
            right -= 1
        if s[left].lower() != s[right].lower():
            return False
        left += 1
        right -= 1
    return True
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
bool isPalindrome(string s) {
    int left = 0, right = s.size() - 1;
    while (left < right) {
        while (left < right && !isalnum(s[left])) left++;
        while (left < right && !isalnum(s[right])) right--;
        if (tolower(s[left]) != tolower(s[right])) return false;
        left++; right--;
    }
    return true;
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Solution 2 — Valid Anagram

> **Problem:** Do two strings use the exact same letters?
> **Weapon used:** the frequency array `int[26]`. Count up for A, count down for B; all zero → anagram.

<details>
<summary>☕ Java</summary>

```java
boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;
    int[] count = new int[26];
    for (int i = 0; i < s.length(); i++) {
        count[s.charAt(i) - 'a']++;
        count[t.charAt(i) - 'a']--;
    }
    for (int c : count) if (c != 0) return false;
    return true;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def is_anagram(s, t):
    if len(s) != len(t):
        return False
    count = [0] * 26
    for i in range(len(s)):
        count[ord(s[i]) - ord('a')] += 1
        count[ord(t[i]) - ord('a')] -= 1
    return all(c == 0 for c in count)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
bool isAnagram(string s, string t) {
    if (s.size() != t.size()) return false;
    int count[26] = {0};
    for (int i = 0; i < s.size(); i++) {
        count[s[i] - 'a']++;
        count[t[i] - 'a']--;
    }
    for (int c : count) if (c != 0) return false;
    return true;
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Solution 3 — First Unique Character in a String

> **Problem:** Return the **index** of the first non-repeating character. If none, return `-1`.
> **Weapon used:** the frequency array `int[26]` + the `c - 'a'` trick.

**The plan (2 passes):**
1. Walk the string once and **count** every character.
2. Walk it again and return the **first index** whose count is exactly 1.

<details>
<summary>☕ Java</summary>

```java
class Solution {
    public int firstUniqChar(String s) {
        int[] freq = new int[26];
        for (int i = 0; i < s.length(); i++) {
            freq[s.charAt(i) - 'a']++;          // pass 1: count
        }
        for (int i = 0; i < s.length(); i++) {
            if (freq[s.charAt(i) - 'a'] == 1) {  // pass 2: first count of 1
                return i;
            }
        }
        return -1;                               // no unique char
    }
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
class Solution:
    def firstUniqChar(self, s):
        freq = [0] * 26
        for ch in s:
            freq[ord(ch) - ord('a')] += 1        # pass 1: count
        for i in range(len(s)):
            if freq[ord(s[i]) - ord('a')] == 1:  # pass 2: first count of 1
                return i
        return -1                                # no unique char
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
class Solution {
public:
    int firstUniqChar(string s) {
        int freq[26] = {0};
        for (char ch : s) {
            freq[ch - 'a']++;                    // pass 1: count
        }
        for (int i = 0; i < s.size(); i++) {
            if (freq[s[i] - 'a'] == 1) {         // pass 2: first count of 1
                return i;
            }
        }
        return -1;                               // no unique char
    }
};
```
</details>

> ⏱️ **Time:** O(n) · **Space:** O(1) (the array is always 26 boxes, no matter how long the string is)

**Dry run — `"leetcode"`:**

| Char | Count |
|------|-------|
| l | 1 |
| e | 3 |
| t | 1 |
| c | 1 |
| o | 1 |
| d | 1 |

Pass 2: index 0 is `l`, count = 1 → **return 0** ✅

> 🧠 **Pattern learned:** Frequency Array + Character Counting + String Traversal. This same 2-pass shape solves a huge family of string problems.

---

## Solution 4 — Reverse String (array of chars)

> **Problem:** Reverse a list of characters in place, O(1) extra memory.
> **Weapon used:** two pointers swapping the two ends.

<details>
<summary>☕ Java</summary>

```java
void reverseString(char[] s) {
    int left = 0, right = s.length - 1;
    while (left < right) {
        char temp = s[left];
        s[left] = s[right];
        s[right] = temp;
        left++; right--;
    }
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def reverse_string(s):          # s is a list of chars
    left, right = 0, len(s) - 1
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
void reverseString(vector<char>& s) {
    int left = 0, right = s.size() - 1;
    while (left < right) {
        swap(s[left], s[right]);
        left++; right--;
    }
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Solution 5 — Reverse Words in a String

> **Problem:** `"the sky is blue"` → `"blue is sky the"`. Trim extra spaces too.
> **Weapon used:** split into words, reverse the order, join back. (Start with this clean version; the in-place trick comes later.)

<details>
<summary>☕ Java</summary>

```java
String reverseWords(String s) {
    String[] words = s.trim().split("\\s+");   // split on one-or-more spaces
    StringBuilder sb = new StringBuilder();
    for (int i = words.length - 1; i >= 0; i--) {
        sb.append(words[i]);
        if (i > 0) sb.append(" ");
    }
    return sb.toString();
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def reverse_words(s):
    words = s.split()           # split() handles extra spaces automatically
    return " ".join(reversed(words))
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
string reverseWords(string s) {
    stringstream ss(s);
    string word;
    vector<string> words;
    while (ss >> word) words.push_back(word);   // >> skips extra spaces
    string result;
    for (int i = words.size() - 1; i >= 0; i--) {
        result += words[i];
        if (i > 0) result += " ";
    }
    return result;
}
```
</details>

> ⏱️ Time O(n) · Space O(n)

> 🧠 **Pattern learned:** strings are just arrays of characters — two pointers and a count array handle almost everything. You've now seen both weapons used across all 5 problems. 🌟
