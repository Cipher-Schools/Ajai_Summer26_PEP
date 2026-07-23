# 🌳 13 — Trees

> 🌿 **Explain Like I'm 5:** A tree is like your family tree or a company org chart. Each person/role is a **node**. Lines between them are **edges**. The top is the **root**, the bottom has **leaves**, and everyone in between is an **internal node**. A **binary tree** just means each node has at most 2 children. That's the whole idea!

> 💛 Two days here. Day 1 builds the foundation — vocabulary, structure, and the 4 ways to walk a tree. Day 2 is where the real interview patterns click: height, comparing trees, and returning information up from subtrees. Slow and steady — trees reward patience more than any other topic so far.

---

# 🟢 DAY 1 — UNDERSTANDING TREES & TRAVERSALS

## 🤔 Why Trees? (15 min)

> Trees show up everywhere once you look for them:
> - 👪 **Family tree** — parents, children, grandchildren
> - 🏢 **Organization hierarchy** — CEO → managers → employees
> - 🗂️ **File system** — folders containing folders containing files

**The key difference:**

| Structure | Shape | Example |
|-----------|-------|---------|
| Array | Linear (one after another) | `[1,2,3,4]` |
| Linked List | Linear (one after another) | `1→2→3→4` |
| **Tree** | **Hierarchical (branches)** | Org chart, file system |

> 🔑 Arrays and linked lists are a straight line. A tree **branches** — one node can have multiple "next" nodes (its children). That branching is the entire new idea this topic introduces.

---

## 🌿 Tree Terminology (30 min)

> Let's build the vocabulary using this example tree:

```
       1
      / \
     2   3
    / \ / \
   4  5 6  7
```

| Term | Meaning | In the example |
|------|---------|-----------------|
| **Root** | The top node — the only one with no parent | `1` |
| **Parent** | A node with children below it | `2` is parent of `4` and `5` |
| **Child** | A node below a parent | `4` and `5` are children of `2` |
| **Sibling** | Nodes sharing the same parent | `4` and `5` are siblings |
| **Leaf Node** | A node with NO children | `4, 5, 6, 7` |
| **Internal Node** | A node with at least 1 child | `1, 2, 3` |
| **Edge** | The connection/line between a parent and child | the line from `1` to `2` |
| **Depth** | Number of edges from the ROOT down to this node | node `5`: depth = 2 |
| **Height** | Number of edges from this node DOWN to its deepest leaf | node `2`: height = 1 |
| **Level** | Same as depth, but often 1-indexed in casual speech | node `5` is on level 2 (or level 3 if counting from 1) |
| **Subtree** | A node and everything below it, treated as its own smaller tree | node `2` + its children `4,5` is a subtree |

> 🎯 **Quick check — ask yourself before moving on:**
> - Root? → `1`
> - Leaf nodes? → `4, 5, 6, 7`
> - Height of the whole tree? → `2` (root to deepest leaf is 2 edges)
> - Level/depth of node `5`? → `2`
>
> If you can answer all four instantly, the vocabulary has landed. If not, redraw the tree and trace it with your finger.

---

## 🌲 Binary Tree Basics (20 min)

> A **binary tree node** holds a value and two pointers: `left` child and `right` child. Either (or both) can be empty (`null`).

<details open>
<summary>☕ Java</summary>

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int val) {
        this.val = val;
    }
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};
```
</details>

**Building the example tree by hand:**

<details>
<summary>☕ Java</summary>

```java
TreeNode root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);
root.right.left = new TreeNode(6);
root.right.right = new TreeNode(7);
```
</details>

<details>
<summary>🐍 Python</summary>

```python
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
root.left.left = TreeNode(4)
root.left.right = TreeNode(5)
root.right.left = TreeNode(6)
root.right.right = TreeNode(7)
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
TreeNode* root = new TreeNode(1);
root->left = new TreeNode(2);
root->right = new TreeNode(3);
root->left->left = new TreeNode(4);
root->left->right = new TreeNode(5);
root->right->left = new TreeNode(6);
root->right->right = new TreeNode(7);
```
</details>

> 📖 On LeetCode, `TreeNode` is already defined for you — you'll just use it.

---

## 🌳 DFS Traversals (60 min)

> **Traversal = visiting every node exactly once.** DFS (Depth-First Search) goes as deep as possible before backtracking. There are 3 flavors, based on WHEN you process the current node relative to its children.

### Preorder — Root → Left → Right `(LC 144)`

```
preorder(node):
    if node is null: return
    process(node)          <- process FIRST
    preorder(node.left)
    preorder(node.right)
```

**Dry run on our example tree:**
```
       1
      / \
     2   3
    / \ / \
   4  5 6  7

Visit 1 (process) -> go left
Visit 2 (process) -> go left
Visit 4 (process) -> no children, back up
Visit 5 (process) -> no children, back up
back to 2, done -> back to 1, go right
Visit 3 (process) -> go left
Visit 6 (process) -> back up
Visit 7 (process) -> done

Preorder: 1 2 4 5 3 6 7  (correct)
```

<details>
<summary>Java</summary>

```java
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    preorder(root, result);
    return result;
}

private void preorder(TreeNode node, List<Integer> result) {
    if (node == null) return;
    result.add(node.val);          // process FIRST
    preorder(node.left, result);
    preorder(node.right, result);
}
```
</details>

<details>
<summary>Python</summary>

```python
def preorderTraversal(self, root):
    result = []
    self.preorder(root, result)
    return result

def preorder(self, node, result):
    if not node:
        return
    result.append(node.val)        # process FIRST
    self.preorder(node.left, result)
    self.preorder(node.right, result)
```
</details>

<details>
<summary>C++</summary>

```cpp
vector<int> preorderTraversal(TreeNode* root) {
    vector<int> result;
    preorder(root, result);
    return result;
}

void preorder(TreeNode* node, vector<int>& result) {
    if (node == nullptr) return;
    result.push_back(node->val);   // process FIRST
    preorder(node->left, result);
    preorder(node->right, result);
}
```
</details>

> Time O(n), Space O(n) worst case (skewed tree recursion stack), O(log n) average

---

### Inorder — Left → Root → Right `(LC 94)`

```
inorder(node):
    if node is null: return
    inorder(node.left)
    process(node)          <- process IN THE MIDDLE
    inorder(node.right)
```

**Dry run on our example tree:**
```
Go all the way left first: 1->2->4 (4 has no left, so process 4)
back to 2 -> process 2 -> go right to 5 -> process 5
back to 1 -> process 1 -> go right to 3
go left to 6 -> process 6 -> back to 3 -> process 3 -> go right to 7 -> process 7

Inorder: 4 2 5 1 6 3 7  (correct)
```

<details>
<summary>Java</summary>

```java
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    inorder(root, result);
    return result;
}

private void inorder(TreeNode node, List<Integer> result) {
    if (node == null) return;
    inorder(node.left, result);
    result.add(node.val);          // process IN THE MIDDLE
    inorder(node.right, result);
}
```
</details>

<details>
<summary>Python</summary>

```python
def inorderTraversal(self, root):
    result = []
    self.inorder(root, result)
    return result

def inorder(self, node, result):
    if not node:
        return
    self.inorder(node.left, result)
    result.append(node.val)        # process IN THE MIDDLE
    self.inorder(node.right, result)
```
</details>

<details>
<summary>C++</summary>

```cpp
vector<int> inorderTraversal(TreeNode* root) {
    vector<int> result;
    inorder(root, result);
    return result;
}

void inorder(TreeNode* node, vector<int>& result) {
    if (node == nullptr) return;
    inorder(node->left, result);
    result.push_back(node->val);   // process IN THE MIDDLE
    inorder(node->right, result);
}
```
</details>

> Time O(n), Space O(n) worst case

---

### Postorder — Left → Right → Root `(LC 145)`

```
postorder(node):
    if node is null: return
    postorder(node.left)
    postorder(node.right)
    process(node)           <- process LAST
```

**Dry run on our example tree:**
```
Go left: 1->2->4, 4 has no children -> process 4
back to 2 -> go right to 5 -> process 5
back to 2 -> process 2 (both children done)
back to 1 -> go right to 3
go left to 6 -> process 6
go right to 7 -> process 7
back to 3 -> process 3 (both children done)
back to 1 -> process 1 (both children done)

Postorder: 4 5 2 6 7 3 1  (correct)
```

<details>
<summary>Java</summary>

```java
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    postorder(root, result);
    return result;
}

private void postorder(TreeNode node, List<Integer> result) {
    if (node == null) return;
    postorder(node.left, result);
    postorder(node.right, result);
    result.add(node.val);          // process LAST
}
```
</details>

<details>
<summary>Python</summary>

```python
def postorderTraversal(self, root):
    result = []
    self.postorder(root, result)
    return result

def postorder(self, node, result):
    if not node:
        return
    self.postorder(node.left, result)
    self.postorder(node.right, result)
    result.append(node.val)        # process LAST
```
</details>

<details>
<summary>C++</summary>

```cpp
vector<int> postorderTraversal(TreeNode* root) {
    vector<int> result;
    postorder(root, result);
    return result;
}

void postorder(TreeNode* node, vector<int>& result) {
    if (node == nullptr) return;
    postorder(node->left, result);
    postorder(node->right, result);
    result.push_back(node->val);   // process LAST
}
```
</details>

> Time O(n), Space O(n) worst case

> **The trick to remembering all 3:** say "root" out loud when it happens. Pre-ROOT-Left-Right -> root said first. Left-ROOT-Right -> root said in the middle. Left-Right-ROOT -> root said last. The name tells you WHERE the root falls in the sentence.

---

## 🌴 BFS Traversal — Level Order `(LC 102)` (30 min)

> DFS goes deep first. **BFS (Breadth-First Search) goes wide first** — visits the whole level 0, then all of level 1, then level 2, etc. **The tool: a queue.**

```
levelOrder(root):
    queue = [root]
    while queue is not empty:
        size = queue.length          <- freeze how many are on THIS level
        for i in 0..size:
            node = queue.dequeue()
            process(node)
            enqueue node.left, node.right if they exist
```

**Dry run:**
```
       1
      / \
     2   3
    / \ / \
   4  5 6  7

queue=[1] -> process level [1] -> enqueue 2,3
queue=[2,3] -> process level [2,3] -> enqueue 4,5,6,7
queue=[4,5,6,7] -> process level [4,5,6,7] -> no more children

Level order: [[1],[2,3],[4,5,6,7]]  (correct)
```

<details>
<summary>Java</summary>

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int size = queue.size();              // freeze this level's size
        List<Integer> level = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            level.add(node.val);
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        result.add(level);
    }
    return result;
}
```
</details>

<details>
<summary>Python</summary>

```python
from collections import deque

def levelOrder(self, root):
    result = []
    if not root:
        return result

    queue = deque([root])
    while queue:
        size = len(queue)                     # freeze this level's size
        level = []
        for _ in range(size):
            node = queue.popleft()
            level.append(node.val)
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        result.append(level)
    return result
```
</details>

<details>
<summary>C++</summary>

```cpp
vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result;
    if (root == nullptr) return result;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int size = q.size();                  // freeze this level's size
        vector<int> level;
        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front(); q.pop();
            level.push_back(node->val);
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        result.push_back(level);
    }
    return result;
}
```
</details>

> Time O(n), Space O(n)

---

## 🧠 Day 1 Summary

```
Why Trees?         -> Hierarchy, not a straight line
Terminology        -> Root, Parent, Child, Sibling, Leaf, Height, Depth, Level
Structure           -> val + left + right
Preorder            -> Root -> Left -> Right   (root said FIRST)
Inorder              -> Left -> Root -> Right   (root said MIDDLE)
Postorder             -> Left -> Right -> Root  (root said LAST)
Level Order (BFS)      -> Queue, one level at a time
```

## 🎯 Day 1 Practice

| Problem | Difficulty | Link |
|---------|-----------|------|
| Binary Tree Preorder Traversal | Easy | https://leetcode.com/problems/binary-tree-preorder-traversal/ |
| Binary Tree Inorder Traversal | Easy | https://leetcode.com/problems/binary-tree-inorder-traversal/ |
| Binary Tree Postorder Traversal | Easy | https://leetcode.com/problems/binary-tree-postorder-traversal/ |
| Binary Tree Level Order Traversal | Medium | https://leetcode.com/problems/binary-tree-level-order-traversal/ |

**Homework (sets up Day 2):**

| Problem | Difficulty | Link |
|---------|-----------|------|
| Maximum Depth of Binary Tree | Easy | https://leetcode.com/problems/maximum-depth-of-binary-tree/ |
| Same Tree | Easy | https://leetcode.com/problems/same-tree/ |
| Symmetric Tree | Easy | https://leetcode.com/problems/symmetric-tree/ |

---

# 🟡 DAY 2 — TREE PROBLEM SOLVING

> **Quick revision before we start:**
> - DFS vs BFS? -> DFS goes deep first (recursion). BFS goes level by level (queue).
> - Preorder sequence? -> Root, Left, Right
> - Inorder sequence? -> Left, Root, Right
> - Postorder sequence? -> Left, Right, Root

> **Today introduces the 2nd and 3rd core tree patterns:**
> 1. ~~Traversal Pattern~~ (Day 1 done)
> 2. **Recursive Divide-and-Conquer** — solve the left subtree, solve the right subtree, combine
> 3. **Return Information from Subtrees** — a recursive call doesn't just do work, it *hands back* useful info (height, whether balanced, etc.) to its parent

---

## Problem 1 — Maximum Depth of Binary Tree `(LC 104)`

> **Introduces the core recursion pattern for trees.** The depth of a tree = 1 (for the current node) + whichever child subtree is deeper.

```
Pattern:  1 + max(leftHeight, rightHeight)
```

<details>
<summary>Java</summary>

```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;                 // base case: empty tree has depth 0
    int left = maxDepth(root.left);
    int right = maxDepth(root.right);
    return 1 + Math.max(left, right);            // count this node + deeper side
}
```
</details>

<details>
<summary>Python</summary>

```python
def maxDepth(self, root):
    if not root:
        return 0                                 # base case: empty tree has depth 0
    left = self.maxDepth(root.left)
    right = self.maxDepth(root.right)
    return 1 + max(left, right)                  # count this node + deeper side
```
</details>

<details>
<summary>C++</summary>

```cpp
int maxDepth(TreeNode* root) {
    if (root == nullptr) return 0;               // base case: empty tree has depth 0
    int left = maxDepth(root->left);
    int right = maxDepth(root->right);
    return 1 + max(left, right);                  // count this node + deeper side
}
```
</details>

> Time O(n), Space O(h), h = tree height (recursion stack)

---

## Problem 2 — Count Complete Tree Nodes `(LC 222)`

> **Simple recursion — count every node.** `1 (this node) + count(left) + count(right)`.

<details>
<summary>Java</summary>

```java
public int countNodes(TreeNode root) {
    if (root == null) return 0;
    return 1 + countNodes(root.left) + countNodes(root.right);
}
```
</details>

<details>
<summary>Python</summary>

```python
def countNodes(self, root):
    if not root:
        return 0
    return 1 + self.countNodes(root.left) + self.countNodes(root.right)
```
</details>

<details>
<summary>C++</summary>

```cpp
int countNodes(TreeNode* root) {
    if (root == nullptr) return 0;
    return 1 + countNodes(root->left) + countNodes(root->right);
}
```
</details>

> (LeetCode's actual constraint is "complete tree," which allows an O(log squared n) trick — but the simple O(n) recursion above is what you should know cold first.)

> Time O(n), Space O(h)

---

## Problem 3 — Same Tree `(LC 100)`

> **Compare two trees node by node.** Same value AND same left subtree AND same right subtree.

<details>
<summary>Java</summary>

```java
public boolean isSameTree(TreeNode p, TreeNode q) {
    if (p == null && q == null) return true;      // both empty -> same
    if (p == null || q == null) return false;     // one empty, one not -> different
    if (p.val != q.val) return false;              // values differ
    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}
```
</details>

<details>
<summary>Python</summary>

```python
def isSameTree(self, p, q):
    if not p and not q:
        return True                                # both empty -> same
    if not p or not q:
        return False                               # one empty, one not -> different
    if p.val != q.val:
        return False                                # values differ
    return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```
</details>

<details>
<summary>C++</summary>

```cpp
bool isSameTree(TreeNode* p, TreeNode* q) {
    if (p == nullptr && q == nullptr) return true;  // both empty -> same
    if (p == nullptr || q == nullptr) return false;  // one empty, one not -> different
    if (p->val != q->val) return false;               // values differ
    return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
}
```
</details>

> Time O(n), Space O(h)

---

## Problem 4 — Balanced Binary Tree `(LC 110)`

> **Bottom-up recursion — return height WHILE checking balance.** A tree is balanced if, for EVERY node, `|leftHeight - rightHeight| <= 1`.
>
> **The clever trick:** instead of computing height separately from checking balance (which would be slow — O(n squared)), return **-1 as a special "unbalanced found" signal** while computing height. That way one traversal does both jobs.

<details>
<summary>Java</summary>

```java
public boolean isBalanced(TreeNode root) {
    return height(root) != -1;
}

private int height(TreeNode node) {
    if (node == null) return 0;

    int left = height(node.left);
    if (left == -1) return -1;              // left subtree already unbalanced

    int right = height(node.right);
    if (right == -1) return -1;              // right subtree already unbalanced

    if (Math.abs(left - right) > 1) return -1;  // THIS node is unbalanced

    return 1 + Math.max(left, right);         // still balanced -- return real height
}
```
</details>

<details>
<summary>Python</summary>

```python
def isBalanced(self, root):
    return self.height(root) != -1

def height(self, node):
    if not node:
        return 0

    left = self.height(node.left)
    if left == -1:
        return -1                            # left subtree already unbalanced

    right = self.height(node.right)
    if right == -1:
        return -1                            # right subtree already unbalanced

    if abs(left - right) > 1:
        return -1                            # THIS node is unbalanced

    return 1 + max(left, right)              # still balanced -- return real height
```
</details>

<details>
<summary>C++</summary>

```cpp
bool isBalanced(TreeNode* root) {
    return height(root) != -1;
}

int height(TreeNode* node) {
    if (node == nullptr) return 0;

    int left = height(node->left);
    if (left == -1) return -1;               // left subtree already unbalanced

    int right = height(node->right);
    if (right == -1) return -1;               // right subtree already unbalanced

    if (abs(left - right) > 1) return -1;     // THIS node is unbalanced

    return 1 + max(left, right);               // still balanced -- return real height
}
```
</details>

> **Why is this efficient?** Each node is visited exactly once. If we'd computed height and balance as two separate functions, we'd recompute height for every subtree repeatedly — O(n squared). Folding the check into the height computation makes it O(n).

> Time O(n), Space O(h)

---

## Problem 5 — Diameter of Binary Tree `(LC 543)`

> **VERY important interview problem.** The diameter is the longest path between any two nodes — and that path might not pass through the root!
>
> **Key insight:** for EVERY node, the longest path THROUGH that node = `leftHeight + rightHeight`. So compute height recursively, and at every node, update a **global maximum** with `left + right`.

```
Pattern:  diameter = leftHeight + rightHeight  (checked at every node, kept as a running max)
```

<details>
<summary>Java</summary>

```java
class Solution {
    int diameter = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        height(root);
        return diameter;
    }

    private int height(TreeNode node) {
        if (node == null) return 0;

        int left = height(node.left);
        int right = height(node.right);

        diameter = Math.max(diameter, left + right);  // longest path THROUGH this node

        return 1 + Math.max(left, right);               // height still bubbles up normally
    }
}
```
</details>

<details>
<summary>Python</summary>

```python
class Solution:
    def __init__(self):
        self.diameter = 0

    def diameterOfBinaryTree(self, root):
        self.height(root)
        return self.diameter

    def height(self, node):
        if not node:
            return 0

        left = self.height(node.left)
        right = self.height(node.right)

        self.diameter = max(self.diameter, left + right)  # longest path THROUGH this node

        return 1 + max(left, right)                         # height still bubbles up normally
```
</details>

<details>
<summary>C++</summary>

```cpp
class Solution {
public:
    int diameter = 0;

    int diameterOfBinaryTree(TreeNode* root) {
        height(root);
        return diameter;
    }

    int height(TreeNode* node) {
        if (node == nullptr) return 0;

        int left = height(node->left);
        int right = height(node->right);

        diameter = max(diameter, left + right);   // longest path THROUGH this node

        return 1 + max(left, right);                // height still bubbles up normally
    }
};
```
</details>

> **Why a global variable?** The function's RETURN value has to be height (so the parent call can use it). But the diameter isn't necessarily at the root — it could peak at any node deep in the tree. A global variable lets us record the best answer seen anywhere, while the return value keeps doing its own separate job.

> Time O(n), Space O(h)

---

## Problem 6 — Binary Tree Paths `(LC 257)`

> **Root-to-leaf traversal — good recursion practice.** Build up a path string as you recurse; when you hit a leaf, save the completed path.

<details>
<summary>Java</summary>

```java
public List<String> binaryTreePaths(TreeNode root) {
    List<String> result = new ArrayList<>();
    if (root == null) return result;
    dfs(root, "", result);
    return result;
}

private void dfs(TreeNode node, String path, List<String> result) {
    path += node.val;

    if (node.left == null && node.right == null) {  // leaf -> save the path
        result.add(path);
        return;
    }

    if (node.left != null) dfs(node.left, path + "->", result);
    if (node.right != null) dfs(node.right, path + "->", result);
}
```
</details>

<details>
<summary>Python</summary>

```python
def binaryTreePaths(self, root):
    result = []
    if not root:
        return result
    self.dfs(root, "", result)
    return result

def dfs(self, node, path, result):
    path += str(node.val)

    if not node.left and not node.right:      # leaf -> save the path
        result.append(path)
        return

    if node.left:
        self.dfs(node.left, path + "->", result)
    if node.right:
        self.dfs(node.right, path + "->", result)
```
</details>

<details>
<summary>C++</summary>

```cpp
vector<string> binaryTreePaths(TreeNode* root) {
    vector<string> result;
    if (root == nullptr) return result;
    dfs(root, "", result);
    return result;
}

void dfs(TreeNode* node, string path, vector<string>& result) {
    path += to_string(node->val);

    if (node->left == nullptr && node->right == nullptr) {  // leaf -> save the path
        result.push_back(path);
        return;
    }

    if (node->left) dfs(node->left, path + "->", result);
    if (node->right) dfs(node->right, path + "->", result);
}
```
</details>

> Time O(n), Space O(h)

---

## Problem 7 — Path Sum `(LC 112)`

> **Root-to-leaf path where the values add up to a target.** Pattern: subtract the current node's value from the target as you go down. At a leaf, check if the remaining target is exactly 0.

```
Pattern:  target -= root.val
```

<details>
<summary>Java</summary>

```java
public boolean hasPathSum(TreeNode root, int targetSum) {
    if (root == null) return false;

    if (root.left == null && root.right == null)   // leaf -> check exact match
        return targetSum == root.val;

    return hasPathSum(root.left, targetSum - root.val) ||
           hasPathSum(root.right, targetSum - root.val);
}
```
</details>

<details>
<summary>Python</summary>

```python
def hasPathSum(self, root, targetSum):
    if not root:
        return False

    if not root.left and not root.right:            # leaf -> check exact match
        return targetSum == root.val

    return (self.hasPathSum(root.left, targetSum - root.val) or
            self.hasPathSum(root.right, targetSum - root.val))
```
</details>

<details>
<summary>C++</summary>

```cpp
bool hasPathSum(TreeNode* root, int targetSum) {
    if (root == nullptr) return false;

    if (root->left == nullptr && root->right == nullptr)  // leaf -> check exact match
        return targetSum == root->val;

    return hasPathSum(root->left, targetSum - root->val) ||
           hasPathSum(root->right, targetSum - root->val);
}
```
</details>

> Time O(n), Space O(h)

---

## Problem 8 — Binary Tree Right Side View `(LC 199)`

> **What you'd see standing to the right of the tree** — the last node visible on each level.
> **Pattern: BFS level order, take the LAST node of every level.**

<details>
<summary>Java</summary>

```java
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> ans = new ArrayList<>();
    if (root == null) return ans;

    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);

    while (!q.isEmpty()) {
        int size = q.size();
        for (int i = 0; i < size; i++) {
            TreeNode node = q.poll();
            if (i == size - 1)                       // last node in this level
                ans.add(node.val);
            if (node.left != null) q.offer(node.left);
            if (node.right != null) q.offer(node.right);
        }
    }
    return ans;
}
```
</details>

<details>
<summary>Python</summary>

```python
from collections import deque

def rightSideView(self, root):
    ans = []
    if not root:
        return ans

    q = deque([root])
    while q:
        size = len(q)
        for i in range(size):
            node = q.popleft()
            if i == size - 1:                        # last node in this level
                ans.append(node.val)
            if node.left:
                q.append(node.left)
            if node.right:
                q.append(node.right)
    return ans
```
</details>

<details>
<summary>C++</summary>

```cpp
vector<int> rightSideView(TreeNode* root) {
    vector<int> ans;
    if (root == nullptr) return ans;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int size = q.size();
        for (int i = 0; i < size; i++) {
            TreeNode* node = q.front(); q.pop();
            if (i == size - 1)                       // last node in this level
                ans.push_back(node->val);
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
    }
    return ans;
}
```
</details>

> **Alternative approach:** DFS going right-first, recording the first node seen at each new depth. Either works — the level-order approach above is more intuitive for beginners.

> Time O(n), Space O(n)

---

## Problem 9 — Lowest Common Ancestor of a Binary Tree `(LC 236)`

> **Find the deepest node that is an ancestor of BOTH p and q.**
> **Simple intuition:**
> - If the current node IS p or q (or null), return it.
> - Recurse into left and right.
> - If BOTH sides find something -> the CURRENT node is the answer (p and q are on different sides).
> - If only ONE side finds something -> pass that result up.

<details>
<summary>Java</summary>

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q)
        return root;                                    // found one of them (or hit the end)

    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);

    if (left != null && right != null)
        return root;                                     // p and q found on DIFFERENT sides -> this is the LCA

    return left != null ? left : right;                   // only one side found something -- pass it up
}
```
</details>

<details>
<summary>Python</summary>

```python
def lowestCommonAncestor(self, root, p, q):
    if not root or root == p or root == q:
        return root                                       # found one of them (or hit the end)

    left = self.lowestCommonAncestor(root.left, p, q)
    right = self.lowestCommonAncestor(root.right, p, q)

    if left and right:
        return root                                        # p and q found on DIFFERENT sides -> this is the LCA

    return left if left else right                          # only one side found something -- pass it up
```
</details>

<details>
<summary>C++</summary>

```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (root == nullptr || root == p || root == q)
        return root;                                       // found one of them (or hit the end)

    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p, q);

    if (left != nullptr && right != nullptr)
        return root;                                        // p and q found on DIFFERENT sides -> this is the LCA

    return left != nullptr ? left : right;                    // only one side found something -- pass it up
}
```
</details>

> **This is the "Return Information from Subtrees" pattern in its purest form.** Each recursive call doesn't just explore — it reports back "did I find p or q down here?" and the parent uses that report to make its decision.

> Time O(n), Space O(h)

---

## Problem 10 — Construct Binary Tree from Preorder and Inorder `(LC 105)`

> **Rebuild a tree given its preorder and inorder sequences.**
> **Key insight:** Preorder's FIRST element is always the ROOT. Find that value in inorder — everything to its LEFT in inorder is the left subtree, everything to its RIGHT is the right subtree.

```
preorder = [3,9,20,15,7]
inorder  = [9,3,15,20,7]

preorder[0] = 3 -> root
find 3 in inorder -> index 1 -> left subtree = [9], right subtree = [15,20,7]
Recurse on each side using the same trick.
```

<details>
<summary>Java</summary>

```java
class Solution {
    int preIndex = 0;
    Map<Integer, Integer> inorderMap = new HashMap<>();

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        for (int i = 0; i < inorder.length; i++)
            inorderMap.put(inorder[i], i);            // value -> index, for O(1) lookup
        return build(preorder, 0, inorder.length - 1);
    }

    private TreeNode build(int[] preorder, int left, int right) {
        if (left > right) return null;

        int rootVal = preorder[preIndex++];            // next unused preorder value = root
        TreeNode root = new TreeNode(rootVal);

        int mid = inorderMap.get(rootVal);              // split point in inorder

        root.left = build(preorder, left, mid - 1);       // everything left of mid
        root.right = build(preorder, mid + 1, right);      // everything right of mid

        return root;
    }
}
```
</details>

<details>
<summary>Python</summary>

```python
class Solution:
    def buildTree(self, preorder, inorder):
        self.pre_index = 0
        self.inorder_map = {val: i for i, val in enumerate(inorder)}  # value -> index
        return self.build(preorder, 0, len(inorder) - 1)

    def build(self, preorder, left, right):
        if left > right:
            return None

        root_val = preorder[self.pre_index]              # next unused preorder value = root
        self.pre_index += 1
        root = TreeNode(root_val)

        mid = self.inorder_map[root_val]                   # split point in inorder

        root.left = self.build(preorder, left, mid - 1)       # everything left of mid
        root.right = self.build(preorder, mid + 1, right)      # everything right of mid

        return root
```
</details>

<details>
<summary>C++</summary>

```cpp
class Solution {
public:
    int preIndex = 0;
    unordered_map<int,int> inorderMap;

    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        for (int i = 0; i < inorder.size(); i++)
            inorderMap[inorder[i]] = i;                   // value -> index
        return build(preorder, 0, inorder.size() - 1);
    }

    TreeNode* build(vector<int>& preorder, int left, int right) {
        if (left > right) return nullptr;

        int rootVal = preorder[preIndex++];                // next unused preorder value = root
        TreeNode* root = new TreeNode(rootVal);

        int mid = inorderMap[rootVal];                      // split point in inorder

        root->left = build(preorder, left, mid - 1);          // everything left of mid
        root->right = build(preorder, mid + 1, right);         // everything right of mid

        return root;
    }
};
```
</details>

> **The HashMap is the O(1) speedup** — without it, finding the root's index in inorder would be an O(n) scan every time, making the whole thing O(n squared).

> Time O(n), Space O(n)

---

## Problem 11 — Construct Binary Tree from Inorder and Postorder `(LC 106)`

> **Same idea as LC 105, but the root comes from the END of postorder** (postorder processes root LAST). **Process the RIGHT subtree first** since we're consuming postorder from the back.

<details>
<summary>Java</summary>

```java
class Solution {
    int postIndex;
    Map<Integer, Integer> inorderMap = new HashMap<>();

    public TreeNode buildTree(int[] inorder, int[] postorder) {
        postIndex = postorder.length - 1;                  // start from the END
        for (int i = 0; i < inorder.length; i++)
            inorderMap.put(inorder[i], i);
        return build(postorder, 0, inorder.length - 1);
    }

    private TreeNode build(int[] postorder, int left, int right) {
        if (left > right) return null;

        int rootVal = postorder[postIndex--];               // next unused value FROM THE END = root
        TreeNode root = new TreeNode(rootVal);

        int mid = inorderMap.get(rootVal);

        root.right = build(postorder, mid + 1, right);        // RIGHT subtree built first!
        root.left = build(postorder, left, mid - 1);

        return root;
    }
}
```
</details>

<details>
<summary>Python</summary>

```python
class Solution:
    def buildTree(self, inorder, postorder):
        self.post_index = len(postorder) - 1              # start from the END
        self.inorder_map = {val: i for i, val in enumerate(inorder)}
        return self.build(postorder, 0, len(inorder) - 1)

    def build(self, postorder, left, right):
        if left > right:
            return None

        root_val = postorder[self.post_index]               # next unused value FROM THE END = root
        self.post_index -= 1
        root = TreeNode(root_val)

        mid = self.inorder_map[root_val]

        root.right = self.build(postorder, mid + 1, right)     # RIGHT subtree built first!
        root.left = self.build(postorder, left, mid - 1)

        return root
```
</details>

<details>
<summary>C++</summary>

```cpp
class Solution {
public:
    int postIndex;
    unordered_map<int,int> inorderMap;

    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        postIndex = postorder.size() - 1;                  // start from the END
        for (int i = 0; i < inorder.size(); i++)
            inorderMap[inorder[i]] = i;
        return build(postorder, 0, inorder.size() - 1);
    }

    TreeNode* build(vector<int>& postorder, int left, int right) {
        if (left > right) return nullptr;

        int rootVal = postorder[postIndex--];                // next unused value FROM THE END = root
        TreeNode* root = new TreeNode(rootVal);

        int mid = inorderMap[rootVal];

        root->right = build(postorder, mid + 1, right);         // RIGHT subtree built first!
        root->left = build(postorder, left, mid - 1);

        return root;
    }
};
```
</details>

> Time O(n), Space O(n)

---

## Problem 12 — Construct Binary Tree from Preorder and Postorder `(LC 889)`

> **The hardest of the three construction problems.** Preorder's first element is the root. Preorder's SECOND element is the root of the LEFT subtree — find that value in postorder to know how big the left subtree is.

<details>
<summary>Java</summary>

```java
class Solution {
    int preIndex = 0;

    public TreeNode constructFromPrePost(int[] preorder, int[] postorder) {
        return build(preorder, postorder, 0, postorder.length - 1);
    }

    private TreeNode build(int[] preorder, int[] postorder, int postStart, int postEnd) {
        if (postStart > postEnd) return null;

        TreeNode root = new TreeNode(preorder[preIndex++]);   // next preorder value = root

        if (postStart == postEnd) return root;                 // single node, no children

        int leftRootVal = preorder[preIndex];                   // preorder's next value = left subtree's root
        int leftSize = 0;
        for (int i = postStart; i <= postEnd; i++) {
            if (postorder[i] == leftRootVal) {
                leftSize = i - postStart + 1;                     // size of left subtree
                break;
            }
        }

        root.left = build(preorder, postorder, postStart, postStart + leftSize - 1);
        root.right = build(preorder, postorder, postStart + leftSize, postEnd - 1);

        return root;
    }
}
```
</details>

<details>
<summary>Python</summary>

```python
class Solution:
    def constructFromPrePost(self, preorder, postorder):
        self.pre_index = 0
        return self.build(preorder, postorder, 0, len(postorder) - 1)

    def build(self, preorder, postorder, post_start, post_end):
        if post_start > post_end:
            return None

        root = TreeNode(preorder[self.pre_index])          # next preorder value = root
        self.pre_index += 1

        if post_start == post_end:
            return root                                       # single node, no children

        left_root_val = preorder[self.pre_index]              # preorder's next value = left subtree's root
        left_size = 0
        for i in range(post_start, post_end + 1):
            if postorder[i] == left_root_val:
                left_size = i - post_start + 1                # size of left subtree
                break

        root.left = self.build(preorder, postorder, post_start, post_start + left_size - 1)
        root.right = self.build(preorder, postorder, post_start + left_size, post_end - 1)

        return root
```
</details>

<details>
<summary>C++</summary>

```cpp
class Solution {
public:
    int preIndex = 0;

    TreeNode* constructFromPrePost(vector<int>& preorder, vector<int>& postorder) {
        return build(preorder, postorder, 0, postorder.size() - 1);
    }

    TreeNode* build(vector<int>& preorder, vector<int>& postorder, int postStart, int postEnd) {
        if (postStart > postEnd) return nullptr;

        TreeNode* root = new TreeNode(preorder[preIndex++]);   // next preorder value = root

        if (postStart == postEnd) return root;                   // single node, no children

        int leftRootVal = preorder[preIndex];                     // preorder's next value = left subtree's root
        int leftSize = 0;
        for (int i = postStart; i <= postEnd; i++) {
            if (postorder[i] == leftRootVal) {
                leftSize = i - postStart + 1;                       // size of left subtree
                break;
            }
        }

        root->left = build(preorder, postorder, postStart, postStart + leftSize - 1);
        root->right = build(preorder, postorder, postStart + leftSize, postEnd - 1);

        return root;
    }
};
```
</details>

> **This one is tricky — expect to re-read it a few times.** The core move: preorder's 2nd element tells you WHO starts the left subtree, and finding that value's position in postorder tells you HOW BIG the left subtree is.

> Time O(n squared) worst case (linear search for leftRootVal — can be optimized to O(n) with a hashmap), Space O(n)

---

## Problem 13 — Maximum Binary Tree `(LC 654)`

> **Build a tree where the largest element becomes the root, recursively.** Classic divide & conquer.

**Brute force:** scan for the max every time (shown below). **Optimized discussion:** a monotonic stack can build this in O(n) — worth exploring once the recursive version is second nature.

<details>
<summary>Java</summary>

```java
public TreeNode constructMaximumBinaryTree(int[] nums) {
    return build(nums, 0, nums.length - 1);
}

private TreeNode build(int[] nums, int left, int right) {
    if (left > right) return null;

    int maxIndex = left;
    for (int i = left; i <= right; i++) {         // find the biggest value in this range
        if (nums[i] > nums[maxIndex])
            maxIndex = i;
    }

    TreeNode root = new TreeNode(nums[maxIndex]);
    root.left = build(nums, left, maxIndex - 1);    // everything left of max
    root.right = build(nums, maxIndex + 1, right);   // everything right of max

    return root;
}
```
</details>

<details>
<summary>Python</summary>

```python
def constructMaximumBinaryTree(self, nums):
    return self.build(nums, 0, len(nums) - 1)

def build(self, nums, left, right):
    if left > right:
        return None

    max_index = left
    for i in range(left, right + 1):              # find the biggest value in this range
        if nums[i] > nums[max_index]:
            max_index = i

    root = TreeNode(nums[max_index])
    root.left = self.build(nums, left, max_index - 1)     # everything left of max
    root.right = self.build(nums, max_index + 1, right)    # everything right of max

    return root
```
</details>

<details>
<summary>C++</summary>

```cpp
TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
    return build(nums, 0, nums.size() - 1);
}

TreeNode* build(vector<int>& nums, int left, int right) {
    if (left > right) return nullptr;

    int maxIndex = left;
    for (int i = left; i <= right; i++) {          // find the biggest value in this range
        if (nums[i] > nums[maxIndex])
            maxIndex = i;
    }

    TreeNode* root = new TreeNode(nums[maxIndex]);
    root->left = build(nums, left, maxIndex - 1);    // everything left of max
    root->right = build(nums, maxIndex + 1, right);   // everything right of max

    return root;
}
```
</details>

> Time O(n squared) worst case (skewed input, e.g. sorted array), Space O(n)

---

## 🧠 Day 2 Summary

```
LC 104   Maximum Depth       ->  1 + max(leftHeight, rightHeight)
LC 222   Count Nodes          ->  1 + count(left) + count(right)
LC 100   Same Tree             ->  compare value + left + right recursively
LC 110   Balanced Tree           ->  return -1 as "unbalanced" signal while computing height
LC 543   Diameter                 ->  leftHeight + rightHeight, tracked as a GLOBAL max
LC 257   Binary Tree Paths          ->  build path string, save at every leaf
LC 112   Path Sum                    ->  target -= root.val, check ==0 at leaf
LC 199   Right Side View               ->  BFS level order, keep the LAST node per level
LC 236   Lowest Common Ancestor          ->  found on both sides -> this node is the LCA
LC 105   Build from Pre + In              ->  preorder[0] = root, split via inorder index
LC 106   Build from In + Post              ->  postorder[last] = root, build RIGHT side first
LC 889   Build from Pre + Post               ->  preorder[1] = left subtree's root, size from postorder
LC 654   Maximum Binary Tree                   ->  largest value = root, recurse both sides
```

> **The 3 core tree patterns you now know:**
> 1. **Traversal Pattern** — walk every node (pre/in/post/level order)
> 2. **Recursive Divide-and-Conquer** — solve left, solve right, combine
> 3. **Return Information from Subtrees** — recursive calls report USEFUL DATA upward (height, balance status, whether p/q were found), not just "done"
>
> These three patterns cover the large majority of beginner-to-intermediate tree questions you'll see in interviews.

---

# 🎯 Practice

**Day 1 — Foundations:**

| Problem | Difficulty | Link | Key Idea |
|---------|-----------|------|----------|
| Binary Tree Preorder Traversal | Easy | https://leetcode.com/problems/binary-tree-preorder-traversal/ | Root -> Left -> Right |
| Binary Tree Inorder Traversal | Easy | https://leetcode.com/problems/binary-tree-inorder-traversal/ | Left -> Root -> Right |
| Binary Tree Postorder Traversal | Easy | https://leetcode.com/problems/binary-tree-postorder-traversal/ | Left -> Right -> Root |
| Binary Tree Level Order Traversal | Medium | https://leetcode.com/problems/binary-tree-level-order-traversal/ | BFS, queue, one level at a time |

**Day 2 — Problem Solving:**

| Problem | Difficulty | Link | Key Idea |
|---------|-----------|------|----------|
| Maximum Depth of Binary Tree | Easy | https://leetcode.com/problems/maximum-depth-of-binary-tree/ | 1 + max(left, right) |
| Count Complete Tree Nodes | Easy | https://leetcode.com/problems/count-complete-tree-nodes/ | 1 + count(left) + count(right) |
| Same Tree | Easy | https://leetcode.com/problems/same-tree/ | Compare value + both subtrees |
| Balanced Binary Tree | Easy | https://leetcode.com/problems/balanced-binary-tree/ | Return -1 signal while computing height |
| Diameter of Binary Tree | Easy | https://leetcode.com/problems/diameter-of-binary-tree/ | leftHeight + rightHeight, global max |
| Binary Tree Paths | Easy | https://leetcode.com/problems/binary-tree-paths/ | Build path string, save at leaves |
| Path Sum | Easy | https://leetcode.com/problems/path-sum/ | target -= root.val |
| Binary Tree Right Side View | Medium | https://leetcode.com/problems/binary-tree-right-side-view/ | BFS, keep last node per level |
| Lowest Common Ancestor of a Binary Tree | Medium | https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/ | Found on both sides -> this is the LCA |
| Construct Binary Tree from Preorder and Inorder | Medium | https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/ | preorder[0]=root, split via inorder |
| Construct Binary Tree from Inorder and Postorder | Medium | https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/ | postorder[last]=root, right side first |
| Construct Binary Tree from Preorder and Postorder | Hard | https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/ | preorder[1]=left subtree root |
| Maximum Binary Tree | Medium | https://leetcode.com/problems/maximum-binary-tree/ | Largest value = root, recurse both sides |

> 🌟 **Solve Day 1 top to bottom until traversals feel automatic — you'll use them constantly.** Then Day 2 builds the real interview muscle: recursion that returns USEFUL information, not just "done." Diameter (LC 543) and LCA (LC 236) are the two most commonly asked in real interviews — know them cold. I'm right here for any doubt. 💪 — *Ajai Raj (Mentor)*
