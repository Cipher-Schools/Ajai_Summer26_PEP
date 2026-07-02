# ☕ Java Syntax for DSA — Your Cheat Sheet

> Keep this open while solving. Every syntax you need for arrays, strings, maps, and sets — with the "why" so it sticks. No need to memorize; just look it up until it's muscle memory.

---

## 1. The Boilerplate (every program starts here)

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        // your code here
        System.out.println("Hello");
    }
}
```

- `import java.util.*;` → brings in ArrayList, HashMap, HashSet, Arrays, Collections. **Always add this for DSA.**
- `System.out.println(x)` → print with a new line. `System.out.print(x)` → no new line.

---

## 2. Variables & Types

```java
int a = 5;               // whole number
long big = 1000000000L;   // huge whole number (note the L)
double d = 3.14;          // decimal
char c = 'a';             // single character (single quotes!)
boolean flag = true;      // true / false
String s = "hello";       // text (double quotes!)
```

> ⚠️ `'a'` (char, single quotes) vs `"a"` (String, double quotes) — a classic beginner mix-up.

---

## 3. Arrays

```java
int[] arr = new int[5];              // 5 zeros: [0,0,0,0,0]
int[] arr = {10, 20, 30};            // direct values
int n = arr.length;                  // size (NO brackets — it's a field, not length())
arr[0] = 99;                         // set
int x = arr[2];                      // read

Arrays.fill(arr, 1);                 // fill all with 1
Arrays.sort(arr);                    // sort ascending
int[] copy = arr.clone();            // copy an array

// 2D array
int[][] grid = new int[3][4];        // 3 rows, 4 columns
grid[1][2] = 7;
```

> 🔑 Array size is `arr.length` (no parentheses). String length is `s.length()` (with parentheses). Java is inconsistent here — just remember it.

---

## 4. Loops

```java
// standard for
for (int i = 0; i < n; i++) { ... }

// for-each (read-only walk)
for (int x : arr) { ... }

// while
while (condition) { ... }

// loop backwards
for (int i = n - 1; i >= 0; i--) { ... }
```

---

## 5. Strings

```java
String s = "hello";
int len = s.length();                // length WITH ()
char c = s.charAt(2);                // character at index 2
String sub = s.substring(1, 4);      // chars from index 1 to 3 (4 excluded)
boolean eq = s.equals("hello");      // compare content — NEVER use == for strings!
char[] arr = s.toCharArray();        // string → char array
String back = new String(arr);       // char array → string
String up = s.toUpperCase();
boolean has = s.contains("ell");
```

> ⚠️ **Compare strings with `.equals()`, not `==`.** `==` checks if they're the same object, not the same text.

### Building strings in a loop → use StringBuilder

```java
StringBuilder sb = new StringBuilder();
sb.append("a");
sb.append(c);
String result = sb.toString();       // convert back when done
```

> 🔑 **Why?** `String` is immutable. Doing `s = s + c` in a loop is secretly O(n²). StringBuilder is O(n).

---

## 6. The `char` ↔ `int` Trick (crucial for strings)

```java
int pos = c - 'a';                   // 'a'→0, 'b'→1, ... 'z'→25
char back = (char) ('a' + pos);      // 0→'a', 1→'b', ...
int digit = c - '0';                 // '7' → 7  (char digit to real number)
```

Used for the 26-size frequency array:
```java
int[] freq = new int[26];
freq[c - 'a']++;                     // count this letter
```

---

## 7. HashMap (key → value) — counting & mapping

```java
HashMap<Character, Integer> map = new HashMap<>();

map.put('a', 1);                     // add / overwrite
map.get('a');                        // read (returns null if missing!)
map.containsKey('a');                // check existence
map.remove('a');
map.size();

// ⭐ getOrDefault — THE counting shortcut you asked about
map.put(c, map.getOrDefault(c, 0) + 1);
// means: "get count of c, or 0 if not there, then add 1"
// without it you'd write:
//   if (map.containsKey(c)) map.put(c, map.get(c) + 1);
//   else map.put(c, 1);
// getOrDefault does both in one clean line.

// loop over a map
for (Map.Entry<Character, Integer> e : map.entrySet()) {
    char key = e.getKey();
    int val = e.getValue();
}
for (char key : map.keySet()) { ... }    // just keys
```

---

## 8. HashSet (unique items) — "have I seen this?"

```java
HashSet<Integer> set = new HashSet<>();

set.add(5);                          // add (duplicates ignored automatically)
set.contains(5);                     // seen it?
set.remove(5);
set.size();

for (int x : set) { ... }            // loop over it
```

---

## 9. ArrayList (a resizable array / list)

```java
List<Integer> list = new ArrayList<>();

list.add(10);                        // append
list.get(0);                         // read by index
list.set(0, 99);                     // overwrite
list.size();
list.remove(0);                      // remove by index
list.contains(10);
Collections.sort(list);              // sort ascending
Collections.sort(list, (a, b) -> b - a);   // sort descending (custom order)
```

> 🔑 **Array vs ArrayList:** array = fixed size, fast. ArrayList = grows automatically, more flexible. Use ArrayList when you don't know the size ahead of time.

---

## 10. Sorting with Custom Order (comparators)

```java
Arrays.sort(arr);                            // ascending (primitives only ascending)
Collections.sort(list);                      // ascending
Collections.sort(list, (a, b) -> a - b);     // ascending
Collections.sort(list, (a, b) -> b - a);     // descending

// sort by map value (e.g. Sort Characters By Frequency)
List<Character> chars = new ArrayList<>(map.keySet());
chars.sort((a, b) -> map.get(b) - map.get(a));   // highest count first
```

> 🧠 **Reading a comparator:** `(a, b) -> a - b` means "ascending." Flip to `b - a` for "descending." That's the whole trick.

---

## 11. Handy Math & Utilities

```java
Math.max(a, b);   Math.min(a, b);   Math.abs(x);
Math.pow(2, 3);                      // returns double 8.0
Integer.MAX_VALUE;  Integer.MIN_VALUE;   // for min/max tracking
String.valueOf(123);                 // number → string
Integer.parseInt("123");             // string → number
```

---

## 12. Reading Input (for online judges / GfG)

```java
Scanner sc = new Scanner(System.in);
int n = sc.nextInt();                // read one int
String word = sc.next();             // read one word
String line = sc.nextLine();         // read whole line
```

---

> 🎯 **You don't need to memorize this.** Solve with this file open. After ~10 problems, 90% of it becomes automatic. Ask me any line that's unclear. 💪
