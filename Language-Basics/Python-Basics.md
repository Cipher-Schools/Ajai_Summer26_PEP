# 🐍 Python Syntax for DSA — Your Cheat Sheet

> Keep this open while solving. Python is the shortest of the three languages — this covers everything you need for arrays, strings, dicts, and sets.

---

## 1. The Basics (no boilerplate needed!)

```python
print("Hello")              # print with new line
print(a, b)                 # print multiple values
x = int(input())            # read one integer
words = input().split()     # read a line, split into words
```

> 🔑 Python needs **no** `main` function or imports for basic code. Just write and run.

---

## 2. Variables (no type declarations)

```python
a = 5                       # int
d = 3.14                    # float
c = 'a'                     # Python has no separate char — it's a 1-length string
flag = True                 # note the capital T (and False)
s = "hello"                 # string
```

> ⚠️ `True`/`False`/`None` are capitalized in Python (unlike `true`/`false` in Java/C++).

---

## 3. Lists (Python's array)

```python
arr = [10, 20, 30]
arr = [0] * 5               # five zeros: [0,0,0,0,0]
n = len(arr)                # size
arr[0] = 99                 # set
x = arr[2]                  # read

arr.append(40)              # add to end
arr.pop()                   # remove & return last
arr.sort()                  # sort ascending (in place)
arr.sort(reverse=True)      # sort descending
arr.reverse()               # reverse in place
total = sum(arr)            # sum of all
biggest = max(arr)          # largest
smallest = min(arr)         # smallest

# 2D list (grid)
grid = [[0] * 4 for _ in range(3)]   # 3 rows, 4 cols
grid[1][2] = 7
```

> ⚠️ **Careful:** `[[0]*4]*3` is a trap — it makes 3 copies of the *same* row. Always use `[[0]*4 for _ in range(3)]`.

---

## 4. Loops

```python
for i in range(n):              # 0 to n-1
    ...
for i in range(1, n):           # 1 to n-1
    ...
for i in range(n-1, -1, -1):    # backwards: n-1 down to 0
    ...
for x in arr:                   # for-each
    ...
for i, x in enumerate(arr):     # index AND value together
    ...
while condition:
    ...
```

> 🔑 `range(start, stop, step)` — `stop` is **excluded**. `range(1,5)` gives 1,2,3,4.

---

## 5. Slicing (Python's superpower)

```python
s[1:4]        # chars from index 1 to 3 (4 excluded)
s[:3]         # first 3 chars
s[2:]         # from index 2 to end
s[::-1]       # REVERSED (whole thing backwards) — famous trick!
arr[::-1]     # reversed list
```

---

## 6. Strings

```python
s = "hello"
len(s)                      # length
s[2]                        # character at index 2
s.upper()   s.lower()
s.split()                   # "a b c" → ['a','b','c']
"".join(list_of_chars)      # ['a','b'] → "ab"
s == "hello"                # compare content — == works fine in Python
'ell' in s                  # substring check → True
s.isalnum()                 # is it letters/numbers only?
list(s)                     # string → list of chars
```

---

## 7. The `char` ↔ `int` Trick (crucial for strings)

```python
pos = ord(c) - ord('a')     # 'a'→0, 'b'→1, ... 'z'→25
back = chr(ord('a') + pos)  # 0→'a', 1→'b', ...
digit = int(c)              # '7' → 7

# 26-size frequency list
freq = [0] * 26
freq[ord(c) - ord('a')] += 1
```

> 🔑 Python uses `ord()` (char → number) and `chr()` (number → char), where Java/C++ just do `c - 'a'`.

---

## 8. Dictionaries (key → value) — counting & mapping

```python
mp = {}

mp['a'] = 1                 # add / overwrite
mp['a']                     # read (ERROR if missing — see below)
'a' in mp                   # check existence
del mp['a']
len(mp)

# ⭐ counting — the getOrDefault equivalent:
mp[c] = mp.get(c, 0) + 1    # "get c, or 0 if missing, then +1"

# loop over a dict
for key in mp:              # keys
    ...
for key, val in mp.items(): # keys AND values
    ...
```

### Even easier: Counter (auto-counting dict)

```python
from collections import Counter

freq = Counter("hello")     # {'l':2, 'h':1, 'e':1, 'o':1} automatically!
freq['l']                   # 2
freq.most_common()          # [('l',2), ('h',1), ...] sorted by count!
freq.most_common(1)         # top 1

# Counter math (used in Find Common Characters):
Counter("bella") & Counter("label")   # keeps the MINIMUM of each key
```

> 🔑 **`Counter` is Python's secret weapon** for frequency problems. It replaces a whole counting loop.

---

## 9. Sets (unique items) — "have I seen this?"

```python
seen = set()

seen.add(5)                 # add (duplicates ignored)
5 in seen                   # seen it?
seen.remove(5)
len(seen)

for x in seen:
    ...

# quick duplicate check:
len(set(arr)) != len(arr)   # True if there are duplicates
```

---

## 10. Sorting with Custom Order

```python
arr.sort()                          # ascending
arr.sort(reverse=True)              # descending
sorted(arr)                         # returns a NEW sorted list

# sort by a custom key
words.sort(key=len)                 # by length
words.sort(key=lambda w: -len(w))   # by length, descending

# sort dict items by value (descending)
sorted(mp.items(), key=lambda x: -x[1])
```

> 🧠 **`key=lambda x: ...`** tells Python *what* to sort by. Add a `-` (or `reverse=True`) to flip the order.

---

## 11. Handy Utilities

```python
max(a, b)   min(a, b)   abs(x)
a, b = b, a                 # swap in one line
float('inf')                # infinity (for min-tracking)
float('-inf')               # negative infinity (for max-tracking)
str(123)                    # number → string
int("123")                  # string → number
```

---

## 12. Functions

```python
def solve(nums, target):
    # ... do work ...
    return answer

# call it
result = solve([1,2,3], 5)
```

> On LeetCode you'll write methods inside a `class Solution:` with `self` as the first parameter — that's just their format, the logic is the same.

---

> 🎯 **Python does more with less** — `Counter`, slicing (`s[::-1]`), and `sorted(key=...)` save you loops. Keep this open while solving, and it'll click within a handful of problems. Ask me anytime. 💪
