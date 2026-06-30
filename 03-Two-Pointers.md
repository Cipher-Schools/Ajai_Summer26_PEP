# 🤝 03 — Two Pointers

> **Explain Like I'm 5:** Imagine two fingers — one on the **left** end, one on the **right** end of the array. They walk toward each other and meet in the middle. That's the two-pointer technique. It's one of the most powerful beginner tricks in all of DSA.

```
[ 1, 2, 3, 4, 5 ]
  ↑           ↑
 left       right     → they move toward each other
```

---

## Use 1 — Reverse an Array (in place)

**Idea:** Swap the two ends, then step both pointers inward. Repeat until they meet.

<details>
<summary>☕ Java</summary>

```java
int left = 0, right = arr.length - 1;
while (left < right) {
    int temp = arr[left];               // swap the two ends
    arr[left] = arr[right];
    arr[right] = temp;
    left++;                             // step inward
    right--;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
left, right = 0, len(arr) - 1
while left < right:
    arr[left], arr[right] = arr[right], arr[left]   # swap (Python makes this easy!)
    left += 1
    right -= 1
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int left = 0, right = n - 1;
while (left < right) {
    swap(arr[left], arr[right]);        // built-in swap
    left++;
    right--;
}
```
</details>

> ⏱️ **Time:** O(n) · **Space:** O(1). We touch each element once and use no extra array.

---

## Use 2 — Pair With Target Sum (on a SORTED array)

> **Problem:** Given a *sorted* array, is there a pair that adds up to a target?
> **Trick:** If the sum is too small, move `left` right (to get bigger). If too big, move `right` left (to get smaller).

<details>
<summary>☕ Java</summary>

```java
int left = 0, right = arr.length - 1;
while (left < right) {
    int sum = arr[left] + arr[right];
    if (sum == target) return true;     // found the pair!
    else if (sum < target) left++;      // need a bigger sum
    else right--;                       // need a smaller sum
}
return false;
```
</details>

<details>
<summary>🐍 Python</summary>

```python
left, right = 0, len(arr) - 1
while left < right:
    s = arr[left] + arr[right]
    if s == target:
        return True                     # found the pair!
    elif s < target:
        left += 1                       # need a bigger sum
    else:
        right -= 1                      # need a smaller sum
return False
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int left = 0, right = n - 1;
while (left < right) {
    int sum = arr[left] + arr[right];
    if (sum == target) return true;     // found the pair!
    else if (sum < target) left++;      // need a bigger sum
    else right--;                       // need a smaller sum
}
return false;
```
</details>

> ⏱️ **Time:** O(n) · **Space:** O(1). Compare this to checking every pair, which is O(n²) — the two-pointer trick is the optimization.

---

## 🎯 Practice (Easy → Easy-Medium)

| Problem | Where | Link |
|---------|-------|------|
| Reverse String (array of chars) | LeetCode | https://leetcode.com/problems/reverse-string/ |
| Two Sum II — Input Array Is Sorted | LeetCode | https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/ |
| Squares of a Sorted Array | LeetCode | https://leetcode.com/problems/squares-of-a-sorted-array/ |
| Move Zeroes | LeetCode | https://leetcode.com/problems/move-zeroes/ |
| Remove Duplicates from Sorted Array | LeetCode | https://leetcode.com/problems/remove-duplicates-from-sorted-array/ |

> 💡 **Start with "Reverse String"** — it's the gentlest two-pointer problem on LeetCode. Once it clicks, the rest follow the same shape. You've got this. 🙌

---

# ✅ Worked Solutions

> All three languages for each. Notice how often the *same two-pointer shape* keeps coming back.

## Solution 1 — Reverse String (array of chars)

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

## Solution 2 — Two Sum II (sorted array)

> **Idea:** Sum too small? Move `left` right. Too big? Move `right` left. (Answer expects 1-based indices.)

<details>
<summary>☕ Java</summary>

```java
int[] twoSum(int[] numbers, int target) {
    int left = 0, right = numbers.length - 1;
    while (left < right) {
        int sum = numbers[left] + numbers[right];
        if (sum == target) return new int[]{left + 1, right + 1};
        else if (sum < target) left++;
        else right--;
    }
    return new int[]{-1, -1};
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def two_sum(numbers, target):
    left, right = 0, len(numbers) - 1
    while left < right:
        s = numbers[left] + numbers[right]
        if s == target:
            return [left + 1, right + 1]
        elif s < target:
            left += 1
        else:
            right -= 1
    return [-1, -1]
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
vector<int> twoSum(vector<int>& numbers, int target) {
    int left = 0, right = numbers.size() - 1;
    while (left < right) {
        int sum = numbers[left] + numbers[right];
        if (sum == target) return {left + 1, right + 1};
        else if (sum < target) left++;
        else right--;
    }
    return {-1, -1};
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Solution 3 — Squares of a Sorted Array

> **Idea:** Negatives squared can be large. The biggest square is always at one of the two ends. Fill the result array from the **back**.

<details>
<summary>☕ Java</summary>

```java
int[] sortedSquares(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    int left = 0, right = n - 1, pos = n - 1;
    while (left <= right) {
        int ls = nums[left] * nums[left];
        int rs = nums[right] * nums[right];
        if (ls > rs) { result[pos--] = ls; left++; }
        else         { result[pos--] = rs; right--; }
    }
    return result;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def sorted_squares(nums):
    n = len(nums)
    result = [0] * n
    left, right, pos = 0, n - 1, n - 1
    while left <= right:
        ls, rs = nums[left] ** 2, nums[right] ** 2
        if ls > rs:
            result[pos] = ls; left += 1
        else:
            result[pos] = rs; right -= 1
        pos -= 1
    return result
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
vector<int> sortedSquares(vector<int>& nums) {
    int n = nums.size(), left = 0, right = n - 1, pos = n - 1;
    vector<int> result(n);
    while (left <= right) {
        int ls = nums[left] * nums[left];
        int rs = nums[right] * nums[right];
        if (ls > rs) { result[pos--] = ls; left++; }
        else         { result[pos--] = rs; right--; }
    }
    return result;
}
```
</details>

> ⏱️ Time O(n) · Space O(n)

---

## Solution 4 — Move Zeroes

> **Idea:** A "slow" pointer marks where the next non-zero goes. A "fast" pointer scans. Swap non-zeros forward; zeroes drift to the end.

<details>
<summary>☕ Java</summary>

```java
void moveZeroes(int[] nums) {
    int slow = 0;
    for (int fast = 0; fast < nums.length; fast++) {
        if (nums[fast] != 0) {
            int temp = nums[slow];
            nums[slow] = nums[fast];
            nums[fast] = temp;
            slow++;
        }
    }
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def move_zeroes(nums):
    slow = 0
    for fast in range(len(nums)):
        if nums[fast] != 0:
            nums[slow], nums[fast] = nums[fast], nums[slow]
            slow += 1
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
void moveZeroes(vector<int>& nums) {
    int slow = 0;
    for (int fast = 0; fast < nums.size(); fast++) {
        if (nums[fast] != 0) {
            swap(nums[slow], nums[fast]);
            slow++;
        }
    }
}
```
</details>

> ⏱️ Time O(n) · Space O(1)

---

## Solution 5 — Remove Duplicates from Sorted Array

> **Idea:** A slow pointer marks the last unique value. When fast finds something new, write it just after slow.

<details>
<summary>☕ Java</summary>

```java
int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;
    int slow = 0;
    for (int fast = 1; fast < nums.length; fast++) {
        if (nums[fast] != nums[slow]) {
            slow++;
            nums[slow] = nums[fast];
        }
    }
    return slow + 1;        // length of unique part
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def remove_duplicates(nums):
    if not nums:
        return 0
    slow = 0
    for fast in range(1, len(nums)):
        if nums[fast] != nums[slow]:
            slow += 1
            nums[slow] = nums[fast]
    return slow + 1
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int removeDuplicates(vector<int>& nums) {
    if (nums.empty()) return 0;
    int slow = 0;
    for (int fast = 1; fast < nums.size(); fast++) {
        if (nums[fast] != nums[slow]) {
            slow++;
            nums[slow] = nums[fast];
        }
    }
    return slow + 1;
}
```
</details>

> ⏱️ Time O(n) · Space O(1). This "slow/fast pointer" pair is the same idea as Move Zeroes — spot the pattern! 🎯
