# ⚡ C++ Syntax for DSA — Your Cheat Sheet

> Keep this open while solving. Includes the tricky bits you mentioned — `sort(rbegin, rend)`, maps, sets — all explained with the "why."

---

## 1. The Boilerplate (every program starts here)

```cpp
#include <bits/stdc++.h>     // includes EVERYTHING (vector, map, set, algorithm...)
using namespace std;         // so you write cout, not std::cout

int main() {
    // your code here
    cout << "Hello" << endl;
    return 0;
}
```

> 🔑 `#include <bits/stdc++.h>` is a shortcut that pulls in all standard libraries at once. Perfect for practice/contests. (Real projects use specific includes, but for DSA this is fine.)

---

## 2. Variables & Types

```cpp
int a = 5;                   // whole number
long long big = 1000000000;  // huge whole number (use for big sums!)
double d = 3.14;             // decimal
char c = 'a';                // single character (single quotes)
bool flag = true;            // true / false
string s = "hello";          // text (double quotes)
```

> ⚠️ Use `long long` when sums might exceed ~2 billion, or your answer silently overflows.

---

## 3. Printing & Reading

```cpp
cout << x << endl;           // print with new line
cout << a << " " << b << "\n";  // multiple values

cin >> x;                    // read one value
cin >> a >> b;               // read two values
```

---

## 4. Vectors (the C++ "array" you'll actually use)

```cpp
vector<int> v;               // empty
vector<int> v(5);            // 5 zeros
vector<int> v(5, 1);         // five 1's
vector<int> v = {10, 20, 30};// direct values

v.push_back(99);             // append to end
v.size();                    // number of elements
v[0] = 5;                    // set
int x = v[2];                // read
v.pop_back();                // remove last

// loop
for (int i = 0; i < v.size(); i++) { ... }
for (int x : v) { ... }      // for-each

// 2D vector (grid)
vector<vector<int>> grid(3, vector<int>(4, 0));  // 3x4 of zeros
grid[1][2] = 7;
```

> 🔑 Plain C-arrays (`int arr[5]`) exist, but **`vector` is preferred** — it knows its own size and can grow.

---

## 5. Loops

```cpp
for (int i = 0; i < n; i++) { ... }        // standard
for (int x : v) { ... }                     // for-each
for (int i = n - 1; i >= 0; i--) { ... }    // backwards
while (condition) { ... }
```

---

## 6. Strings

```cpp
string s = "hello";
s.size();  // or s.length()   — both work
s[2];                        // character at index 2 (like an array)
s.substr(1, 3);              // 3 chars starting at index 1
s + "world";                 // concatenation (this is fine in C++)
s.push_back('!');            // add a char to the end
reverse(s.begin(), s.end()); // reverse in place
sort(s.begin(), s.end());    // sort the characters
s == "hello";                // comparing strings with == WORKS in C++ (unlike Java!)
```

> ✅ Unlike Java, in C++ you **can** use `==` to compare string contents. And `s + t` is fine.

---

## 7. The `char` ↔ `int` Trick (crucial for strings)

```cpp
int pos = c - 'a';                   // 'a'→0, 'b'→1, ... 'z'→25
char back = 'a' + pos;               // 0→'a', 1→'b', ...
int digit = c - '0';                 // '7' → 7

// 26-size frequency array
vector<int> freq(26, 0);
freq[c - 'a']++;                     // count this letter
```

---

## 8. unordered_map (key → value) — counting & mapping

```cpp
unordered_map<char, int> mp;

mp['a'] = 1;                         // add / overwrite
mp['a'];                             // read (auto-creates as 0 if missing!)
mp.count('a');                       // 1 if key exists, else 0
mp.erase('a');
mp.size();

// ⭐ counting — C++ is easy here:
mp[c]++;                             // if c is new, it starts at 0 then becomes 1
// This is C++'s version of Java's getOrDefault — the [] auto-inserts 0.

// loop over a map
for (auto p : mp) {
    char key = p.first;
    int val = p.second;
}
```

> 🔑 **Java's `getOrDefault(c, 0) + 1` = C++'s simple `mp[c]++`.** In C++, accessing a missing key auto-creates it with value 0, so `mp[c]++` just works. Easier than Java here!

---

## 9. unordered_set (unique items) — "have I seen this?"

```cpp
unordered_set<int> st;

st.insert(5);                        // add (duplicates ignored)
st.count(5);                         // 1 if present, else 0
st.erase(5);
st.size();

for (int x : st) { ... }             // loop
```

---

## 10. Sorting — including the `rbegin/rend` you asked about

```cpp
sort(v.begin(), v.end());            // ascending (smallest first)
sort(v.rbegin(), v.rend());          // DESCENDING (largest first)
```

> 🧠 **What are `begin/end` and `rbegin/rend`?**
> - `v.begin()` points to the **first** element, `v.end()` just past the **last**. Sorting between them → normal ascending order.
> - `v.rbegin()` / `v.rend()` are the **reversed** versions — they walk the vector backwards. Sorting "backwards" gives you **descending** order. That's the whole trick — no custom function needed.

```cpp
// custom sort (e.g. sort pairs by first value descending)
vector<pair<int,char>> arr;
sort(arr.rbegin(), arr.rend());      // sorts pairs by .first, then .second, descending

// custom comparator (full control)
sort(v.begin(), v.end(), [](int a, int b) {
    return a > b;                    // "a comes before b if a > b" → descending
});
```

> 🔑 **Reading a comparator:** `return a > b;` means descending. `return a < b;` means ascending. The comparator answers "should `a` come before `b`?"

---

## 11. Handy Utilities

```cpp
max(a, b);   min(a, b);   abs(x);
swap(a, b);                          // swap two variables
INT_MAX;   INT_MIN;                  // for min/max tracking
to_string(123);                      // number → string
stoi("123");                         // string → number
*max_element(v.begin(), v.end());    // biggest in a vector
*min_element(v.begin(), v.end());    // smallest in a vector
accumulate(v.begin(), v.end(), 0);   // sum of a vector (needs <numeric>)
```

---

## 12. Pairs (bundling two values)

```cpp
pair<int, char> p = {5, 'a'};
p.first;    // 5
p.second;   // 'a'

vector<pair<int,int>> vp;
vp.push_back({3, 4});
```

---

> 🎯 **Key takeaway:** C++ is often *shorter* than Java for hashing (`mp[c]++`) and descending sort (`sort(v.rbegin(), v.rend())`). Keep this file open, and those two lines will stop being scary fast. Ask me anytime. 💪
