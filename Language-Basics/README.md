# 🧰 Language Basics — Syntax References

> **Stuck on syntax, not logic?** This folder is for you. Whenever you know *what* to do but forget *how to write it* — how to make a map, count frequencies, sort descending — look here.

| File | For | Highlights |
|------|-----|-----------|
| `Java-Basics.md` | Java users | `getOrDefault`, StringBuilder, comparators, `char - 'a'` |
| `Cpp-Basics.md` | C++ users | `mp[c]++`, `sort(rbegin, rend)`, vectors, pairs |
| `Python-Basics.md` | Python users | `Counter`, slicing `s[::-1]`, `sorted(key=...)` |

---

## How To Use This

1. Pick **your** language file and skim it once — just so you know what's in it.
2. While solving a problem, keep it open in a second tab.
3. Forgot how to sort descending? Ctrl+F "descending." Done.

> 🎯 **You don't memorize syntax — you look it up until your fingers remember.** Every good programmer keeps a reference handy. This is yours.

---

### Quick "same idea, three languages" comparison

**Counting how many times each item appears:**

```java
// Java
map.put(c, map.getOrDefault(c, 0) + 1);
```
```cpp
// C++  (easiest — [] auto-creates 0)
mp[c]++;
```
```python
# Python (easiest — use Counter)
freq = Counter(s)
```

**Sorting descending:**

```java
// Java
Collections.sort(list, (a, b) -> b - a);
```
```cpp
// C++
sort(v.rbegin(), v.rend());
```
```python
# Python
arr.sort(reverse=True)
```

> See how each language has its own "shortcut"? Once you know your language's shortcuts, DSA gets much smoother. 💪
