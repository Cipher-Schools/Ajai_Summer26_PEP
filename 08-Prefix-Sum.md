# ➕ 08 — Prefix Sum

> 🧠 **The whole idea in one line:**
> **Without prefix sum → I keep recalculating the past.**
> **With prefix sum → I remember previous work and reuse it forever.**

> 💛 Don't memorize a formula here. Feel the *shift*: stop redoing old addition, store it once. That mental switch is the entire topic.

---

## The Bank Account Story (Explain Like I'm 5)

> 💰 You deposit `1, 2, 3, 4` on four days. Your **running total** after each day is:
> ```
> Day 1: 1
> Day 2: 1+2 = 3
> Day 3: 1+2+3 = 6
> Day 4: 1+2+3+4 = 10
> ```
> Notice Day 3 doesn't re-add Day 1 and Day 2 from scratch — it just takes yesterday's total and adds today. **That reuse is prefix sum.**

---

## The Ladder (Each Problem Upgrades the Last)

```
1480  →  Build Prefix Sum
1732  →  Prefix Sum + Maximum
 724  →  Prefix Sum + Balance
2574  →  Prefix Sum + Difference
1413  →  Prefix Sum + Minimum
 238  →  Prefix Product (left × right)
```

---

## Problem 1 — Running Sum of 1D Array `(LC 1480)`

> **Build the prefix sum.** Each value becomes itself + the running total before it.
> `[1,2,3,4] → [1,3,6,10]`

<details>
<summary>☕ Java</summary>

```java
public int[] runningSum(int[] nums) {
    for (int i = 1; i < nums.length; i++) {
        nums[i] += nums[i - 1];        // add yesterday's total
    }
    return nums;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def runningSum(self, nums):
    for i in range(1, len(nums)):
        nums[i] += nums[i - 1]         # add yesterday's total
    return nums
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
vector<int> runningSum(vector<int>& nums) {
    for (int i = 1; i < nums.size(); i++)
        nums[i] += nums[i - 1];        // add yesterday's total
    return nums;
}
```
</details>

> ⏱️ **Time:** O(n) · **Space:** O(1)

---

## Problem 2 — Find Highest Altitude `(LC 1732)`

> **Teaching line: Running Sum + Maximum.** A cyclist starts at altitude 0. Each `gain` moves them up/down. Track the running altitude AND the highest it ever reaches.

```
gain = [-5, 1, 5, 0, -7]
altitude: 0 → -5 → -4 → 1 → 1 → -6
highest reached: 1
```

<details>
<summary>☕ Java</summary>

```java
public int largestAltitude(int[] gain) {
    int altitude = 0, max = 0;
    for (int g : gain) {
        altitude += g;                 // running sum
        max = Math.max(max, altitude); // track the peak
    }
    return max;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def largestAltitude(self, gain):
    altitude = 0
    max_alt = 0
    for g in gain:
        altitude += g                  # running sum
        max_alt = max(max_alt, altitude)  # track the peak
    return max_alt
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int largestAltitude(vector<int>& gain) {
    int altitude = 0, mx = 0;
    for (int g : gain) {
        altitude += g;                 // running sum
        mx = max(mx, altitude);        // track the peak
    }
    return mx;
}
```
</details>

> ⏱️ **Time:** O(n) · **Space:** O(1)

---

## Problem 3 — Find Pivot Index `(LC 724)`

> **See-saw story:** find the index where **left sum == right sum**.
> **Prefix insight:** if you know the `total` and the `left` sum so far, the right side is instant: `right = total - left - nums[i]`. No re-looping!

```
[1,7,3,6,5,6] → pivot at index 3
left  = 1+7+3 = 11
right = 5+6   = 11  ✅
```

<details>
<summary>☕ Java</summary>

```java
public int pivotIndex(int[] nums) {
    int total = 0;
    for (int num : nums) total += num;      // grand total

    int left = 0;
    for (int i = 0; i < nums.length; i++) {
        int right = total - left - nums[i];  // right side, instantly
        if (left == right) return i;
        left += nums[i];                     // grow the left sum
    }
    return -1;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def pivotIndex(self, nums):
    total = sum(nums)                        # grand total
    left = 0
    for i in range(len(nums)):
        right = total - left - nums[i]       # right side, instantly
        if left == right:
            return i
        left += nums[i]                      # grow the left sum
    return -1
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int pivotIndex(vector<int>& nums) {
    int total = 0;
    for (int num : nums) total += num;       // grand total

    int left = 0;
    for (int i = 0; i < nums.size(); i++) {
        int right = total - left - nums[i];  // right side, instantly
        if (left == right) return i;
        left += nums[i];                     // grow the left sum
    }
    return -1;
}
```
</details>

> ⏱️ **Time:** O(n) · **Space:** O(1). Brute force would be O(n²) — the prefix trick is the upgrade.

---

## Problem 4 — Left and Right Sum Differences `(LC 2574)`

> **Same as Pivot Index — but now save every `|left - right|`** into an answer array.
> `[10,4,8,3] → [15,1,11,22]`

<details>
<summary>☕ Java</summary>

```java
public int[] leftRightDifference(int[] nums) {
    int total = 0;
    for (int num : nums) total += num;

    int left = 0;
    int[] ans = new int[nums.length];
    for (int i = 0; i < nums.length; i++) {
        int right = total - left - nums[i];
        ans[i] = Math.abs(left - right);     // save the difference
        left += nums[i];
    }
    return ans;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def leftRightDifference(self, nums):
    total = sum(nums)
    left = 0
    ans = []
    for i in range(len(nums)):
        right = total - left - nums[i]
        ans.append(abs(left - right))        # save the difference
        left += nums[i]
    return ans
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
vector<int> leftRightDifference(vector<int>& nums) {
    int total = 0;
    for (int num : nums) total += num;

    int left = 0;
    vector<int> ans(nums.size());
    for (int i = 0; i < nums.size(); i++) {
        int right = total - left - nums[i];
        ans[i] = abs(left - right);          // save the difference
        left += nums[i];
    }
    return ans;
}
```
</details>

> ⏱️ **Time:** O(n) · **Space:** O(n) (for the answer array)

---

## Problem 5 — Minimum Start Value `(LC 1413)`

> 🎮 **Health bar story:** you start with `X` health. Each step adds/subtracts. Health must **never drop below 1**. Find the smallest `X`.
> **Key observation:** find the *lowest* the running sum ever gets. Then `X = 1 - lowest`.

```
[-3, 2, -3, 4, 2]  →  running: -3, -1, -4, 0, 2
lowest = -4  →  answer = 1 - (-4) = 5
```

<details>
<summary>☕ Java</summary>

```java
public int minStartValue(int[] nums) {
    int prefix = 0, minPrefix = 0;
    for (int num : nums) {
        prefix += num;                       // running sum
        minPrefix = Math.min(minPrefix, prefix);  // lowest point
    }
    return 1 - minPrefix;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def minStartValue(self, nums):
    prefix = 0
    min_prefix = 0
    for num in nums:
        prefix += num                        # running sum
        min_prefix = min(min_prefix, prefix) # lowest point
    return 1 - min_prefix
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int minStartValue(vector<int>& nums) {
    int prefix = 0, minPrefix = 0;
    for (int num : nums) {
        prefix += num;                       // running sum
        minPrefix = min(minPrefix, prefix);  // lowest point
    }
    return 1 - minPrefix;
}
```
</details>

> ⏱️ **Time:** O(n) · **Space:** O(1)

---

## Problem 6 — Product of Array Except Self `(LC 238)`

> **The masterpiece.** Each position = product of everything *except itself*, and you can't use division.
> **Genius idea:** multiply everything to the **left**, then everything to the **right**. Two passes.

```
nums  = [1, 2, 3, 4]
left  = [1, 1, 2, 6]     (product of everything before i)
right = [24,12, 4, 1]    (product of everything after i)
answer= [24,12, 8, 6]    (left × right)
```

<details>
<summary>☕ Java</summary>

```java
public int[] productExceptSelf(int[] nums) {
    int n = nums.length;
    int[] ans = new int[n];

    ans[0] = 1;
    for (int i = 1; i < n; i++)
        ans[i] = ans[i - 1] * nums[i - 1];   // left products

    int right = 1;
    for (int i = n - 1; i >= 0; i--) {
        ans[i] *= right;                     // multiply in right product
        right *= nums[i];
    }
    return ans;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def productExceptSelf(self, nums):
    n = len(nums)
    ans = [1] * n

    for i in range(1, n):
        ans[i] = ans[i - 1] * nums[i - 1]    # left products

    right = 1
    for i in range(n - 1, -1, -1):
        ans[i] *= right                      # multiply in right product
        right *= nums[i]
    return ans
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
vector<int> productExceptSelf(vector<int>& nums) {
    int n = nums.size();
    vector<int> ans(n);

    ans[0] = 1;
    for (int i = 1; i < n; i++)
        ans[i] = ans[i - 1] * nums[i - 1];   // left products

    int right = 1;
    for (int i = n - 1; i >= 0; i--) {
        ans[i] *= right;                     // multiply in right product
        right *= nums[i];
    }
    return ans;
}
```
</details>

> ⏱️ **Time:** O(n) · **Space:** O(1) (output array doesn't count as extra)

---

## 🧠 End-Class Summary (The Board)

```
1480  →  Build Prefix Sum
1732  →  Prefix Sum + Maximum
 724  →  Prefix Sum + Balance
2574  →  Prefix Sum + Difference
1413  →  Prefix Sum + Minimum
 238  →  Prefix Product
```

> ⭐ **Golden line:** *Instead of recalculating the past, store it once and reuse it forever.*
> Carry this feeling into **Sliding Window** next — it's the same "don't redo work" spirit.

---

# 🎯 Practice

| # | Problem | Difficulty | Link |
|---|---------|-----------|------|
| 1 | Running Sum of 1d Array | Easy | https://leetcode.com/problems/running-sum-of-1d-array/ |
| 2 | Find the Highest Altitude | Easy | https://leetcode.com/problems/find-the-highest-altitude/ |
| 3 | Find Pivot Index | Easy | https://leetcode.com/problems/find-pivot-index/ |
| 4 | Left and Right Sum Differences | Easy | https://leetcode.com/problems/left-and-right-sum-differences/ |
| 5 | Minimum Value to Get Positive Step by Step Sum | Easy | https://leetcode.com/problems/minimum-value-to-get-positive-step-by-step-sum/ |
| 6 | Product of Array Except Self | Medium | https://leetcode.com/problems/product-of-array-except-self/ |

> 💡 All six are solved above. Do 1→5 in order (each is a tiny upgrade), then attempt 238 — it's the "boss." You've got this. 💪 — *Ajai Raj (Mentor)*
