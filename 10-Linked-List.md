# 🔗 10 — Linked List

> 🚂 **Explain Like I'm 5:** A train. Each coach (node) holds cargo (a value) and is coupled to the **next** coach. You can't jump to coach 5 — you walk from the engine, coach by coach. That's a linked list.

```
[ 1 | • ] → [ 2 | • ] → [ 3 | • ] → [ 4 | null ]
  val next    val next    val next      (end)
 (head)
```

> 🔑 **The #1 difference from arrays:** no index jumping. No `list[3]`. You must *walk* using `.next`.

> 💛 Two days of content here. Day 1 builds the foundation (6 problems). Day 2 combines them into real interview problems (6 more). **These 12 problems cover ~90% of linked-list interview patterns.** Go slow. Draw boxes and arrows on paper for every one.

---

## 📋 The Interview Cheat Sheet (one-glance reference)

| Pattern | Technique | Problems |
|---------|-----------|----------|
| Walk the list | `curr = curr.next` | Traverse, Length, Search |
| Find middle | Slow (1 step) + Fast (2 steps) | Middle, Palindrome |
| Reverse | prev / curr / next | Reverse, Palindrome |
| Detect cycle | Floyd's (slow + fast meet) | Cycle I, Cycle II |
| Build a result list | Dummy node | Merge, Remove Nth, Add Two Numbers |
| Pointer gap | Move fast `n` steps first | Remove Nth From End |
| Carry math | `sum % 10`, `sum / 10` | Add Two Numbers |
| Rearrange pointers | Maintain separate chains | Odd-Even |

---

# 🟢 DAY 1 — FOUNDATIONS

## Problem 1 — Traverse a Linked List

> Visit every node once and print its value. The most basic linked-list loop — you'll write it hundreds of times.

<details>
<summary>☕ Java</summary>

```java
void traverse(ListNode head) {
    ListNode curr = head;
    while (curr != null) {
        System.out.print(curr.val + " ");
        curr = curr.next;               // take one step
    }
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def traverse(head):
    curr = head
    while curr:
        print(curr.val, end=" ")
        curr = curr.next                 # take one step
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
void traverse(ListNode* head) {
    ListNode* curr = head;
    while (curr != nullptr) {
        cout << curr->val << " ";
        curr = curr->next;               // take one step
    }
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Problem 2 — Find Length of Linked List

> Count how many nodes exist. Same loop, just count instead of print.

<details>
<summary>☕ Java</summary>

```java
int length(ListNode head) {
    int count = 0;
    while (head != null) {
        count++;
        head = head.next;
    }
    return count;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def length(head):
    count = 0
    while head:
        count += 1
        head = head.next
    return count
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int length(ListNode* head) {
    int count = 0;
    while (head) {
        count++;
        head = head->next;
    }
    return count;
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Problem 3 — Search Element in Linked List

> Linear search — walk and compare each value to the target.

<details>
<summary>☕ Java</summary>

```java
boolean search(ListNode head, int key) {
    while (head != null) {
        if (head.val == key) return true;
        head = head.next;
    }
    return false;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def search(head, key):
    while head:
        if head.val == key:
            return True
        head = head.next
    return False
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
bool search(ListNode* head, int key) {
    while (head) {
        if (head->val == key) return true;
        head = head->next;
    }
    return false;
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Problem 4 — Middle of the Linked List `(LC 876)` ⭐

> **Trick: slow (1 step) + fast (2 steps).** When fast reaches the end, slow is at the middle. No need to count length first!

```
1 → 2 → 3 → 4 → 5

slow=1  fast=1
slow=2  fast=3
slow=3  fast=5 → fast.next is null → STOP

Middle = 3  ✅
```

<details>
<summary>☕ Java</summary>

```java
public ListNode middleNode(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;              // 1 step
        fast = fast.next.next;         // 2 steps
    }
    return slow;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def middleNode(self, head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next               # 1 step
        fast = fast.next.next          # 2 steps
    return slow
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
ListNode* middleNode(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;             // 1 step
        fast = fast->next->next;       // 2 steps
    }
    return slow;
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Problem 5 — Reverse Linked List `(LC 206)` ⭐⭐

> **The most important linked-list problem.** Three pointers: `prev`, `curr`, `next`. The order never changes: **save → flip → move → move.**

```
Before:  1 → 2 → 3 → 4 → null
After:   null ← 1 ← 2 ← 3 ← 4

Step by step:
prev=null  curr=1
  next=2, flip 1→null, prev=1, curr=2
prev=1     curr=2
  next=3, flip 2→1,    prev=2, curr=3
prev=2     curr=3
  next=4, flip 3→2,    prev=3, curr=4
prev=3     curr=4
  next=null, flip 4→3, prev=4, curr=null → STOP

return prev (which is 4, the new head)
```

<details>
<summary>☕ Java</summary>

```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null, curr = head;
    while (curr != null) {
        ListNode next = curr.next;      // 1. save what's ahead
        curr.next = prev;               // 2. flip the arrow backward
        prev = curr;                    // 3. move prev up
        curr = next;                    // 4. move curr up
    }
    return prev;                        // new head
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def reverseList(self, head):
    prev, curr = None, head
    while curr:
        nxt = curr.next                 # 1. save what's ahead
        curr.next = prev                # 2. flip the arrow backward
        prev = curr                     # 3. move prev up
        curr = nxt                      # 4. move curr up
    return prev                         # new head
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
ListNode* reverseList(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* curr = head;
    while (curr) {
        ListNode* next = curr->next;    // 1. save what's ahead
        curr->next = prev;              // 2. flip the arrow backward
        prev = curr;                    // 3. move prev up
        curr = next;                    // 4. move curr up
    }
    return prev;                        // new head
}
```
</details>

> 🧠 **Say it while you write:** save → flip → move → move. Drill this until your fingers know it.

> ⏱️ Time O(n) · Space O(1)

---

## Problem 6 — Linked List Cycle `(LC 141)` ⭐

> **Floyd's Algorithm.** Slow moves 1 step, fast moves 2 steps. If there's a loop, fast will lap slow and they'll **meet**. If fast hits null, no cycle.

```
1 → 2 → 3 → 4
        ↑    ↓
        └────┘

slow=1 fast=1
slow=2 fast=3
slow=3 fast=2       (fast looped around!)
slow=4 fast=4       → MEET → cycle exists ✅
```

<details>
<summary>☕ Java</summary>

```java
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;  // they met → cycle!
    }
    return false;                       // fast hit null → no cycle
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def hasCycle(self, head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True                 # they met → cycle!
    return False                        # fast hit null → no cycle
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
bool hasCycle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) return true;  // they met → cycle!
    }
    return false;
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## 🟢 Day 1 Summary

```
Traverse     → curr = curr.next
Length        → count++
Search        → linear search walk
Middle        → slow / fast pointer
Reverse       → prev / curr / next (save → flip → move → move)
Cycle Detect  → Floyd's (slow + fast meet)
```

> ✅ If you can write all six from memory, you have the foundation. Day 2 is just *combining* these.

---

# 🟡 DAY 2 — INTERVIEW-LEVEL PROBLEMS

> Every problem below is a **combination** of Day 1 techniques. No new tricks — just mixing the ones you already know.

---

## Problem 7 — Remove Nth Node From End `(LC 19)` ⭐

> **Technique: gap of `n` between two pointers.**
> Move `fast` ahead by `n` steps first. Then move both together. When `fast` hits null, `slow` is right before the target.

```
1 → 2 → 3 → 4 → 5     n = 2

Move fast 2+1 steps (using dummy): fast is at 4
Then walk together:
  slow=1 fast=4
  slow=2 fast=5
  slow=3 fast=null → STOP
  
slow.next = slow.next.next → skip node 4
Result: 1 → 2 → 3 → 5
```

> 💡 **Why a dummy node?** If we need to remove the *head* itself (n = length), there's no node before it. The dummy solves that edge case.

<details>
<summary>☕ Java</summary>

```java
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode slow = dummy, fast = dummy;

    for (int i = 0; i <= n; i++)           // move fast n+1 steps ahead
        fast = fast.next;

    while (fast != null) {                 // walk together
        slow = slow.next;
        fast = fast.next;
    }

    slow.next = slow.next.next;            // skip the target node
    return dummy.next;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def removeNthFromEnd(self, head, n):
    dummy = ListNode(0)
    dummy.next = head
    slow = fast = dummy

    for _ in range(n + 1):                 # move fast n+1 steps ahead
        fast = fast.next

    while fast:                            # walk together
        slow = slow.next
        fast = fast.next

    slow.next = slow.next.next             # skip the target node
    return dummy.next
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* slow = dummy;
    ListNode* fast = dummy;

    for (int i = 0; i <= n; i++)           // move fast n+1 steps ahead
        fast = fast->next;

    while (fast) {                         // walk together
        slow = slow->next;
        fast = fast->next;
    }

    slow->next = slow->next->next;         // skip the target node
    return dummy->next;
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Problem 8 — Merge Two Sorted Lists `(LC 21)` ⭐

> **Technique: dummy node + compare & attach.** Like merging two sorted decks of cards — always pick the smaller top card.

```
l1: 1 → 2 → 4
l2: 1 → 3 → 4

Compare 1 vs 1 → take l1's 1
Compare 2 vs 1 → take l2's 1
Compare 2 vs 3 → take 2
Compare 4 vs 3 → take 3
Compare 4 vs 4 → take l1's 4
l1 done → attach remaining l2: 4

Result: 1 → 1 → 2 → 3 → 4 → 4
```

<details>
<summary>☕ Java</summary>

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode tail = dummy;

    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) {
            tail.next = l1;
            l1 = l1.next;
        } else {
            tail.next = l2;
            l2 = l2.next;
        }
        tail = tail.next;
    }
    tail.next = (l1 != null) ? l1 : l2;   // attach leftovers
    return dummy.next;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def mergeTwoLists(self, l1, l2):
    dummy = ListNode(0)
    tail = dummy

    while l1 and l2:
        if l1.val <= l2.val:
            tail.next = l1
            l1 = l1.next
        else:
            tail.next = l2
            l2 = l2.next
        tail = tail.next

    tail.next = l1 if l1 else l2           # attach leftovers
    return dummy.next
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode dummy(0);
    ListNode* tail = &dummy;

    while (l1 && l2) {
        if (l1->val <= l2->val) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }
    tail->next = l1 ? l1 : l2;            // attach leftovers
    return dummy.next;
}
```
</details>

> ⏱️ Time O(n + m) · Space O(1)

---

## Problem 9 — Add Two Numbers `(LC 2)` ⭐

> **Technique: carry math.** Numbers are stored in reverse order (ones digit first). Walk both lists simultaneously, adding digits + carry.
> **Core formula:** `sum = x + y + carry`, `digit = sum % 10`, `carry = sum / 10`

```
l1: 2 → 4 → 3        (represents 342)
l2: 5 → 6 → 4        (represents 465)

2+5+0 = 7  digit=7 carry=0
4+6+0 = 10 digit=0 carry=1
3+4+1 = 8  digit=8 carry=0

Result: 7 → 0 → 8    (represents 807)   ✅
```

<details>
<summary>☕ Java</summary>

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode tail = dummy;
    int carry = 0;

    while (l1 != null || l2 != null || carry > 0) {
        int sum = carry;
        if (l1 != null) { sum += l1.val; l1 = l1.next; }
        if (l2 != null) { sum += l2.val; l2 = l2.next; }
        tail.next = new ListNode(sum % 10);   // digit
        carry = sum / 10;                      // carry
        tail = tail.next;
    }
    return dummy.next;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def addTwoNumbers(self, l1, l2):
    dummy = ListNode(0)
    tail = dummy
    carry = 0

    while l1 or l2 or carry:
        s = carry
        if l1: s += l1.val; l1 = l1.next
        if l2: s += l2.val; l2 = l2.next
        tail.next = ListNode(s % 10)           # digit
        carry = s // 10                        # carry
        tail = tail.next

    return dummy.next
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode* dummy = new ListNode(0);
    ListNode* tail = dummy;
    int carry = 0;

    while (l1 || l2 || carry) {
        int sum = carry;
        if (l1) { sum += l1->val; l1 = l1->next; }
        if (l2) { sum += l2->val; l2 = l2->next; }
        tail->next = new ListNode(sum % 10);   // digit
        carry = sum / 10;                       // carry
        tail = tail->next;
    }
    return dummy->next;
}
```
</details>

> 🔑 **The `|| carry > 0` in the while condition** handles the final carry (e.g. 99 + 1 = 100 → that last `1` needs a new node).

> ⏱️ Time O(max(n, m)) · Space O(max(n, m))

---

## Problem 10 — Linked List Cycle II `(LC 142)` ⭐

> **Find WHERE the cycle starts.** Step 1: Floyd's to find the meeting point. Step 2: one pointer from `head`, other from meeting point, both move 1 step — where they meet is the cycle start. (The math works out — trust it.)

```
1 → 2 → 3 → 4 → 5
        ↑         ↓
        └─────────┘

Floyd's: slow & fast meet at some node inside the cycle.
Then: p1 starts at head, p2 starts at meeting point.
  p1=1 p2=meeting
  p1=2 p2=...
  p1=3 p2=3 → MEET → cycle starts at 3  ✅
```

<details>
<summary>☕ Java</summary>

```java
public ListNode detectCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) {                // met inside the cycle
            slow = head;                   // reset one to head
            while (slow != fast) {         // both move 1 step now
                slow = slow.next;
                fast = fast.next;
            }
            return slow;                   // meeting point = cycle start
        }
    }
    return null;                           // no cycle
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def detectCycle(self, head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:                   # met inside the cycle
            slow = head                    # reset one to head
            while slow != fast:            # both move 1 step
                slow = slow.next
                fast = fast.next
            return slow                    # cycle start
    return None                            # no cycle
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
ListNode* detectCycle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) {                // met inside the cycle
            slow = head;                   // reset one to head
            while (slow != fast) {         // both move 1 step
                slow = slow->next;
                fast = fast->next;
            }
            return slow;                   // cycle start
        }
    }
    return nullptr;                        // no cycle
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Problem 11 — Palindrome Linked List `(LC 234)` ⭐

> **Combines three Day 1 skills:** find middle → reverse second half → compare both halves.

```
1 → 2 → 2 → 1

Step 1: find middle → split into  1 → 2  |  2 → 1
Step 2: reverse second half →             1 → 2
Step 3: compare  1==1 ✅  2==2 ✅ → palindrome!
```

<details>
<summary>☕ Java</summary>

```java
public boolean isPalindrome(ListNode head) {
    // 1. find middle
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    // 2. reverse second half
    ListNode prev = null, curr = slow;
    while (curr != null) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    // 3. compare both halves
    ListNode left = head, right = prev;
    while (right != null) {
        if (left.val != right.val) return false;
        left = left.next;
        right = right.next;
    }
    return true;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def isPalindrome(self, head):
    # 1. find middle
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    # 2. reverse second half
    prev, curr = None, slow
    while curr:
        nxt = curr.next
        curr.next = prev
        prev = curr
        curr = nxt
    # 3. compare both halves
    left, right = head, prev
    while right:
        if left.val != right.val:
            return False
        left = left.next
        right = right.next
    return True
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
bool isPalindrome(ListNode* head) {
    // 1. find middle
    ListNode* slow = head;
    ListNode* fast = head;
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    // 2. reverse second half
    ListNode* prev = nullptr;
    ListNode* curr = slow;
    while (curr) {
        ListNode* next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    // 3. compare both halves
    ListNode* left = head;
    ListNode* right = prev;
    while (right) {
        if (left->val != right->val) return false;
        left = left->next;
        right = right->next;
    }
    return true;
}
```
</details>

> 🧠 **This is the "combo" problem.** If you can do middle + reverse + traverse, you can do palindrome. It's Day 1 skills stacked.

> ⏱️ Time O(n) · Space O(1)

---

## Problem 12 — Odd Even Linked List `(LC 328)` ⭐

> **Separate odd-positioned and even-positioned nodes into two chains, then join them.** (Position 1, 3, 5… then 2, 4, 6…)

```
1 → 2 → 3 → 4 → 5

Odd chain:  1 → 3 → 5
Even chain: 2 → 4

Join: 1 → 3 → 5 → 2 → 4
```

<details>
<summary>☕ Java</summary>

```java
public ListNode oddEvenList(ListNode head) {
    if (head == null) return null;
    ListNode odd = head;
    ListNode even = head.next;
    ListNode evenHead = even;              // save start of even chain

    while (even != null && even.next != null) {
        odd.next = even.next;              // odd skips to next odd
        odd = odd.next;
        even.next = odd.next;              // even skips to next even
        even = even.next;
    }
    odd.next = evenHead;                   // join chains
    return head;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def oddEvenList(self, head):
    if not head:
        return None
    odd = head
    even = head.next
    even_head = even                       # save start of even chain

    while even and even.next:
        odd.next = even.next               # odd skips to next odd
        odd = odd.next
        even.next = odd.next               # even skips to next even
        even = even.next

    odd.next = even_head                   # join chains
    return head
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
ListNode* oddEvenList(ListNode* head) {
    if (!head) return nullptr;
    ListNode* odd = head;
    ListNode* even = head->next;
    ListNode* evenHead = even;             // save start of even chain

    while (even && even->next) {
        odd->next = even->next;            // odd skips to next odd
        odd = odd->next;
        even->next = odd->next;            // even skips to next even
        even = even->next;
    }
    odd->next = evenHead;                  // join chains
    return head;
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## 🧠 Day 2 Pattern Recognition

```
LC 19    Remove Nth  →  Gap between two pointers + dummy
LC 21    Merge       →  Dummy node + compare & attach
LC 2     Add Numbers →  Carry handling (sum%10, sum/10)
LC 142   Cycle II    →  Floyd + math (head + meeting point)
LC 234   Palindrome  →  Middle + Reverse + Compare
LC 328   Odd-Even    →  Separate chains + join
```

> Every single one uses techniques from Day 1. If a Day 2 problem feels hard, go back and re-drill the Day 1 technique it's built on.

---

# 🎯 Practice (in order)

**Day 1 — Foundations:**

| Problem | Difficulty | Link | Technique |
|---------|-----------|------|-----------|
| Middle of the Linked List | Easy | https://leetcode.com/problems/middle-of-the-linked-list/ | slow / fast |
| Reverse Linked List | Easy | https://leetcode.com/problems/reverse-linked-list/ | prev / curr / next |
| Linked List Cycle | Easy | https://leetcode.com/problems/linked-list-cycle/ | Floyd's |
| Remove Duplicates from Sorted List | Easy | https://leetcode.com/problems/remove-duplicates-from-sorted-list/ | traverse + skip |

**Day 2 — Interview Level:**

| Problem | Difficulty | Link | Technique |
|---------|-----------|------|-----------|
| Remove Nth Node From End of List | Medium | https://leetcode.com/problems/remove-nth-node-from-end-of-list/ | gap + dummy |
| Merge Two Sorted Lists | Easy | https://leetcode.com/problems/merge-two-sorted-lists/ | dummy + compare |
| Add Two Numbers | Medium | https://leetcode.com/problems/add-two-numbers/ | carry math |
| Linked List Cycle II | Medium | https://leetcode.com/problems/linked-list-cycle-ii/ | Floyd + reset |
| Palindrome Linked List | Easy | https://leetcode.com/problems/palindrome-linked-list/ | middle + reverse |
| Odd Even Linked List | Medium | https://leetcode.com/problems/odd-even-linked-list/ | separate chains |

**Bonus (when the above feel easy):**

| Problem | Difficulty | Link | Technique |
|---------|-----------|------|-----------|
| Intersection of Two Linked Lists | Easy | https://leetcode.com/problems/intersection-of-two-linked-lists/ | length diff or two-pass |
| Rotate List | Medium | https://leetcode.com/problems/rotate-list/ | length + connect + break |
| Swap Nodes in Pairs | Medium | https://leetcode.com/problems/swap-nodes-in-pairs/ | pointer rewiring |
| Reorder List | Medium | https://leetcode.com/problems/reorder-list/ | middle + reverse + merge |
| Sort List | Medium | https://leetcode.com/problems/sort-list/ | merge sort on LL |

---

> 🌟 **These 12 core problems cover ~90% of linked-list patterns in placement interviews.** Master Day 1 first — it's the floor. Day 2 is just combinations. Draw every problem on paper. I'm right here for any doubt. 💪 — *Ajai Raj (Mentor)*
