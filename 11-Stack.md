# 🥞 11 — Stack

> 🍽️ **Explain Like I'm 5:** A stack of plates. You can only take the **top** plate off, and you can only put a new plate **on top**. You can never grab a plate from the middle without removing everything above it first.
>
> That's a **Stack** — **LIFO: Last In, First Out.** The last plate you put on is the first one you take off.

```
Top
 ↓
[30]
[20]
[10]
```

---

## The 5 Operations (Memorize These Names)

| Operation | What it does |
|-----------|-------------|
| **Push** | Insert a new item on top |
| **Pop** | Remove the top item |
| **Peek** | Look at the top item (without removing it) |
| **isEmpty** | Check if the stack has nothing in it |
| **isFull** | Check if there's no more space (array version only) |

> 🔑 **Everything about stacks is just these 5 words.** Once they're automatic, every stack problem becomes "which of these 5 do I need right now?"

---

## Implementation 1 — Stack Using Array

> 🧠 **Teaching line: Stack = Array + Top Pointer.**
> The array holds the values. A `top` variable tracks the index of the current top item.

```
Top
 ↓
30   ← index 2
20   ← index 1
10   ← index 0
```

<details>
<summary>☕ Java</summary>

```java
class ArrayStack {
    int[] arr;
    int top;

    ArrayStack(int size) {
        arr = new int[size];
        top = -1;                       // -1 means empty
    }

    boolean isFull() {
        return top == arr.length - 1;
    }

    boolean isEmpty() {
        return top == -1;
    }

    void push(int x) {
        if (isFull()) {
            System.out.println("Stack Overflow");
            return;
        }
        arr[++top] = x;                 // move top up, then insert
    }

    int pop() {
        if (isEmpty()) {
            System.out.println("Stack Underflow");
            return -1;
        }
        return arr[top--];               // read top, then move down
    }

    int peek() {
        if (isEmpty()) return -1;
        return arr[top];
    }
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
class ArrayStack:
    def __init__(self, size):
        self.arr = [0] * size
        self.top = -1                    # -1 means empty

    def is_full(self):
        return self.top == len(self.arr) - 1

    def is_empty(self):
        return self.top == -1

    def push(self, x):
        if self.is_full():
            print("Stack Overflow")
            return
        self.top += 1
        self.arr[self.top] = x           # move top up, then insert

    def pop(self):
        if self.is_empty():
            print("Stack Underflow")
            return -1
        val = self.arr[self.top]         # read top
        self.top -= 1                    # then move down
        return val

    def peek(self):
        if self.is_empty():
            return -1
        return self.arr[self.top]
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
class ArrayStack {
    vector<int> arr;
    int top;
    int capacity;

public:
    ArrayStack(int size) {
        arr.resize(size);
        capacity = size;
        top = -1;                        // -1 means empty
    }

    bool isFull() { return top == capacity - 1; }
    bool isEmpty() { return top == -1; }

    void push(int x) {
        if (isFull()) {
            cout << "Stack Overflow" << endl;
            return;
        }
        arr[++top] = x;                  // move top up, then insert
    }

    int pop() {
        if (isEmpty()) {
            cout << "Stack Underflow" << endl;
            return -1;
        }
        return arr[top--];               // read top, then move down
    }

    int peek() {
        if (isEmpty()) return -1;
        return arr[top];
    }
};
```
</details>

> ⚠️ **Array stacks have a fixed size** — decided when you create them. Push past the limit → **Stack Overflow.**

> ⏱️ All operations: Time O(1) · Space O(n) for the array

---

## Implementation 2 — Stack Using Linked List

> 🧠 **Teaching line: Array Stack = Fixed Size. Linked List Stack = Dynamic Size.**
> No size limit — push adds a new node **at the head**, pop removes **from the head**. (The head IS the top — no walking required, so it's still O(1).)

```
Top
 ↓
[30] → [20] → [10] → null
```

<details>
<summary>☕ Java</summary>

```java
class Node {
    int val;
    Node next;
    Node(int val) { this.val = val; }
}

class LinkedListStack {
    Node top;

    boolean isEmpty() {
        return top == null;
    }

    void push(int x) {
        Node newNode = new Node(x);
        newNode.next = top;              // new node points to old top
        top = newNode;                   // new node becomes the top
    }

    int pop() {
        if (isEmpty()) {
            System.out.println("Stack Underflow");
            return -1;
        }
        int val = top.val;
        top = top.next;                  // top moves down to next node
        return val;
    }

    int peek() {
        if (isEmpty()) return -1;
        return top.val;
    }
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
class Node:
    def __init__(self, val):
        self.val = val
        self.next = None

class LinkedListStack:
    def __init__(self):
        self.top = None

    def is_empty(self):
        return self.top is None

    def push(self, x):
        new_node = Node(x)
        new_node.next = self.top         # new node points to old top
        self.top = new_node              # new node becomes the top

    def pop(self):
        if self.is_empty():
            print("Stack Underflow")
            return -1
        val = self.top.val
        self.top = self.top.next         # top moves down to next node
        return val

    def peek(self):
        if self.is_empty():
            return -1
        return self.top.val
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
struct Node {
    int val;
    Node* next;
    Node(int val) { this->val = val; this->next = nullptr; }
};

class LinkedListStack {
    Node* top = nullptr;

public:
    bool isEmpty() { return top == nullptr; }

    void push(int x) {
        Node* newNode = new Node(x);
        newNode->next = top;             // new node points to old top
        top = newNode;                   // new node becomes the top
    }

    int pop() {
        if (isEmpty()) {
            cout << "Stack Underflow" << endl;
            return -1;
        }
        int val = top->val;
        Node* temp = top;
        top = top->next;                 // top moves down to next node
        delete temp;
        return val;
    }

    int peek() {
        if (isEmpty()) return -1;
        return top->val;
    }
};
```
</details>

> ⏱️ All operations: Time O(1) · Space O(n)

---

## In Real Code, Use the Built-In Stack

> You'll build one by hand once (above) to understand it. After that, use your language's built-in stack:

<details>
<summary>☕ Java</summary>

```java
Deque<Integer> stack = new ArrayDeque<>();  // preferred over old Stack class
stack.push(10);
stack.pop();
stack.peek();
stack.isEmpty();
```
</details>

<details>
<summary>🐍 Python</summary>

```python
stack = []                # a plain list works as a stack!
stack.append(10)          # push
stack.pop()                # pop
stack[-1]                  # peek
len(stack) == 0             # isEmpty
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
stack<int> st;
st.push(10);
st.pop();
st.top();                  // peek
st.empty();                 // isEmpty
```
</details>

---

## 📋 Implementation Comparison

| | Array Stack | Linked List Stack |
|---|-------------|-------------------|
| Size | **Fixed** (decided upfront) | **Dynamic** (grows as needed) |
| Can overflow? | Yes | No (until memory runs out) |
| Speed | O(1) | O(1) |
| Extra memory per item | None | A `next` pointer per node |

---

# 🎯 Applications — Where Stacks Actually Get Used

> 🪄 **The #1 clue a problem wants a stack:** anything about **matching pairs**, **undo history**, or **"most recent thing first."**

---

## Problem 1 — Valid Parentheses `(LC 20)` ⭐

> **Teaching line: Every opening bracket needs a matching closing bracket.**
> **Pattern:** Opening bracket → **push** it. Closing bracket → check if it **matches** the top, then **pop**.

```
"()[]{}"  → valid ✅
"([)]"    → invalid ❌ (brackets cross instead of nesting properly)
```

**Dry run — `"([)]"` (the invalid one):**

```
'(' → push        stack: (
'[' → push        stack: ( [
')' → closing! peek top = '[' → doesn't match ')' → INVALID ❌
```

<details>
<summary>☕ Java</summary>

```java
public boolean isValid(String s) {
    Deque<Character> stack = new ArrayDeque<>();
    for (char c : s.toCharArray()) {
        if (c == '(' || c == '[' || c == '{') {
            stack.push(c);                        // opening → push
        } else {
            if (stack.isEmpty()) return false;     // closing with nothing to match
            char top = stack.pop();
            if (c == ')' && top != '(') return false;
            if (c == ']' && top != '[') return false;
            if (c == '}' && top != '{') return false;
        }
    }
    return stack.isEmpty();                        // nothing left unmatched
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def isValid(self, s):
    stack = []
    pairs = {')': '(', ']': '[', '}': '{'}

    for c in s:
        if c in '([{':
            stack.append(c)                        # opening → push
        else:
            if not stack or stack[-1] != pairs[c]:
                return False                        # no match
            stack.pop()

    return len(stack) == 0                          # nothing left unmatched
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
bool isValid(string s) {
    stack<char> st;
    for (char c : s) {
        if (c == '(' || c == '[' || c == '{') {
            st.push(c);                             // opening → push
        } else {
            if (st.empty()) return false;           // closing with nothing to match
            char top = st.top(); st.pop();
            if (c == ')' && top != '(') return false;
            if (c == ']' && top != '[') return false;
            if (c == '}' && top != '{') return false;
        }
    }
    return st.empty();                              // nothing left unmatched
}
```
</details>

> ⏱️ Time O(n) · Space O(n)

---

## Problem 2 — Minimum Add to Make Parentheses Valid `(LC 921)`

> **Teaching line: Count unmatched brackets.**
> Why after LC 20? Because students already understand "unmatched" from the last problem — this just **counts** instead of returning true/false.

```
"())"  → answer: 1   (need 1 more '(' to fix the extra ')')
```

**Dry run:**
```
'(' → push        openNeeded = 1
')' → matches!    openNeeded = 0
')' → nothing to match! → closeNeeded++ (closeNeeded = 1)

Total additions needed = openNeeded + closeNeeded = 0 + 1 = 1  ✅
```

<details>
<summary>☕ Java</summary>

```java
public int minAddToMakeValid(String s) {
    int openNeeded = 0;    // unmatched '(' we're still waiting to close
    int closeNeeded = 0;   // unmatched ')' with nothing to match

    for (char c : s.toCharArray()) {
        if (c == '(') {
            openNeeded++;
        } else {
            if (openNeeded > 0) openNeeded--;   // this ')' matches an earlier '('
            else closeNeeded++;                 // no '(' waiting → extra ')'
        }
    }
    return openNeeded + closeNeeded;             // total brackets we must add
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def minAddToMakeValid(self, s):
    open_needed = 0        # unmatched '(' we're still waiting to close
    close_needed = 0       # unmatched ')' with nothing to match

    for c in s:
        if c == '(':
            open_needed += 1
        else:
            if open_needed > 0:
                open_needed -= 1                 # matches an earlier '('
            else:
                close_needed += 1                # extra ')'

    return open_needed + close_needed            # total brackets to add
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int minAddToMakeValid(string s) {
    int openNeeded = 0;     // unmatched '(' we're still waiting to close
    int closeNeeded = 0;    // unmatched ')' with nothing to match

    for (char c : s) {
        if (c == '(') {
            openNeeded++;
        } else {
            if (openNeeded > 0) openNeeded--;    // matches an earlier '('
            else closeNeeded++;                  // extra ')'
        }
    }
    return openNeeded + closeNeeded;              // total brackets to add
}
```
</details>

> 🔑 **Why no real stack object here?** We only have ONE type of bracket, so we don't need to check *which* bracket is on top — just *how many* are unmatched. A counter does the job of a stack. (LC 20 needed a real stack because multiple bracket *types* had to match correctly.)

> ⏱️ Time O(n) · Space O(1)

---

## Problem 3 — Minimum Remove to Make Valid Parentheses `(LC 1249)`

> **Teaching line: Instead of checking validity, remove invalid brackets.**
> This is the natural extension of LC 20 — push **indices** of `(` onto the stack. Any `)` with no `(` to match gets marked for removal. Anything left in the stack at the end (unmatched `(`) also gets removed.

```
"lee(t(c)o)de)"  →  "lee(t(c)o)de"
```

**Dry run (tracking indices):**
```
index 3: '(' → push 3          stack: [3]
index 5: '(' → push 5          stack: [3, 5]
index 7: ')' → matches! pop 5   stack: [3]
index 9: ')' → matches! pop 3   stack: []
index 12: ')' → nothing to match → mark index 12 for removal

stack is empty at the end → no leftover '(' to remove
Remove index 12 → "lee(t(c)o)de"  ✅
```

<details>
<summary>☕ Java</summary>

```java
public String minRemoveToMakeValid(String s) {
    Deque<Integer> stack = new ArrayDeque<>();
    Set<Integer> toRemove = new HashSet<>();
    char[] chars = s.toCharArray();

    for (int i = 0; i < chars.length; i++) {
        if (chars[i] == '(') {
            stack.push(i);                       // remember the index
        } else if (chars[i] == ')') {
            if (stack.isEmpty()) toRemove.add(i); // no '(' to match → remove this
            else stack.pop();                     // matched! keep both
        }
    }
    while (!stack.isEmpty()) toRemove.add(stack.pop());  // leftover '(' → remove

    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < chars.length; i++) {
        if (!toRemove.contains(i)) sb.append(chars[i]);
    }
    return sb.toString();
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def minRemoveToMakeValid(self, s):
    stack = []
    to_remove = set()
    chars = list(s)

    for i, c in enumerate(chars):
        if c == '(':
            stack.append(i)                      # remember the index
        elif c == ')':
            if not stack:
                to_remove.add(i)                  # no '(' to match → remove this
            else:
                stack.pop()                       # matched! keep both

    to_remove.update(stack)                       # leftover '(' → remove

    return ''.join(c for i, c in enumerate(chars) if i not in to_remove)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
string minRemoveToMakeValid(string s) {
    stack<int> st;
    unordered_set<int> toRemove;

    for (int i = 0; i < s.size(); i++) {
        if (s[i] == '(') {
            st.push(i);                          // remember the index
        } else if (s[i] == ')') {
            if (st.empty()) toRemove.insert(i);   // no '(' to match → remove
            else st.pop();                        // matched! keep both
        }
    }
    while (!st.empty()) {                         // leftover '(' → remove
        toRemove.insert(st.top());
        st.pop();
    }

    string result;
    for (int i = 0; i < s.size(); i++) {
        if (toRemove.find(i) == toRemove.end()) result += s[i];
    }
    return result;
}
```
</details>

> 🔑 **The upgrade from LC 20:** instead of pushing the *character*, we push the **index**. That way, when we decide something is invalid, we know exactly *where* to remove it from.

> ⏱️ Time O(n) · Space O(n)

---

## 🧠 End of Day 1 Summary

```
Stack Operations:     Push · Pop · Peek · isEmpty · isFull

Implementation:       Array (fixed size)  vs  Linked List (dynamic size)

Applications:
  LC 20    →  Match brackets using a real stack
  LC 921   →  Count unmatched (no stack object needed — just counters)
  LC 1249  →  Push INDICES, remove what's unmatched
```

> ⭐ **The golden line for the whole day:** *A stack lets you always deal with "the most recent thing first" — perfect for anything about matching pairs or undoing the last action.*

---

# 🎯 Practice

| Problem | Difficulty | Link | Key Idea |
|---------|-----------|------|----------|
| Valid Parentheses | Easy | https://leetcode.com/problems/valid-parentheses/ | Push opening, match & pop on closing |
| Minimum Add to Make Parentheses Valid | Medium | https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/ | Count unmatched (no stack object needed) |
| Minimum Remove to Make Valid Parentheses | Medium | https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/ | Push indices, remove what's unmatched |

> 💡 **Do them in this order — LC 20 first.** Once matching brackets clicks, 921 and 1249 are small twists on the same idea, not new mountains. I'm right here for any doubt. 💪 — *Ajai Raj (Mentor)*
