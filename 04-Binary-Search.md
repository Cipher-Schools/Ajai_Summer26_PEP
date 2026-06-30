# 🔍 04 — Binary Search

> **Explain Like I'm 5:** Finding a word in a dictionary. You don't read page 1, 2, 3... You open the **middle**, decide if your word is before or after, and throw away half the book instantly. Repeat. That's binary search — and it's *lightning fast*.

> ⚠️ **One golden rule:** Binary search only works on a **SORTED** array.

```
Find 7 in:  [1, 3, 5, 7, 9, 11]
             low      mid      high
mid = 5 → 7 > 5 → answer is on the RIGHT → throw away the left half → repeat
```

---

## The Core Code

<details>
<summary>☕ Java</summary>

```java
int binarySearch(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;   // safe middle
        if (arr[mid] == target) return mid; // found it!
        else if (arr[mid] < target) low = mid + 1;  // go right
        else high = mid - 1;                // go left
    }
    return -1;                              // not found
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid                       # found it!
        elif arr[mid] < target:
            low = mid + 1                    # go right
        else:
            high = mid - 1                   # go left
    return -1                                # not found
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int binarySearch(int arr[], int n, int target) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;   // safe middle
        if (arr[mid] == target) return mid; // found it!
        else if (arr[mid] < target) low = mid + 1;  // go right
        else high = mid - 1;                // go left
    }
    return -1;                              // not found
}
```
</details>

> ⏱️ **Time:** O(log n) — for 1,00,000 elements, only ~17 steps! · **Space:** O(1)

---

## 🧠 3 Beginner Traps (Read Carefully)

> 1. **The array MUST be sorted.** No exceptions.
> 2. Write `low + (high - low) / 2`, not `(low + high) / 2` — the second one can overflow on huge numbers.
> 3. Use `low <= high` (with the **=**). Forgetting the equals sign is the #1 beginner bug.

---

## Dry Run It (Do This On Paper!)

Find `7` in `[1, 3, 5, 7, 9]`:

| Step | low | high | mid | arr[mid] | Action |
|------|-----|------|-----|----------|--------|
| 1 | 0 | 4 | 2 | 5 | 7 > 5 → go right, low = 3 |
| 2 | 3 | 4 | 3 | 7 | 7 == 7 → **return 3** ✅ |

> Tracing it by hand like this is the fastest way to *truly* understand binary search. Do it once with paper and pen — it'll click.

---

## 🎯 Practice (Start Easy)

| Problem | Where | Link |
|---------|-------|------|
| Binary Search | LeetCode | https://leetcode.com/problems/binary-search/ |
| Search Insert Position | LeetCode | https://leetcode.com/problems/search-insert-position/ |
| First and Last Position of Element | LeetCode | https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/ |
| Floor in a Sorted Array | GfG | https://www.geeksforgeeks.org/problems/floor-in-a-sorted-array-1587115620/1 |
| Search in Rotated Sorted Array | LeetCode | https://leetcode.com/problems/search-in-rotated-sorted-array/ |

> 💡 **Do the first one ("Binary Search") until you can write it without looking.** That single problem is worth a whole day. Everything else here is just a small twist on it. I'm here for any doubt. 🙏

---

# ✅ Worked Solutions

> Every one is just the core binary search with a tiny twist. Spot the same skeleton each time.

## Solution 1 — Binary Search

<details>
<summary>☕ Java</summary>

```java
int search(int[] nums, int target) {
    int low = 0, high = nums.length - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def search(nums, target):
    low, high = 0, len(nums) - 1
    while low <= high:
        mid = (low + high) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int search(vector<int>& nums, int target) {
    int low = 0, high = nums.size() - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}
```
</details>

> ⏱️ Time O(log n) · Space O(1)

---

## Solution 2 — Search Insert Position

> **Idea:** Same search. If not found, `low` ends up exactly where the target *should* be inserted.

<details>
<summary>☕ Java</summary>

```java
int searchInsert(int[] nums, int target) {
    int low = 0, high = nums.length - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return low;          // the insert position
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def search_insert(nums, target):
    low, high = 0, len(nums) - 1
    while low <= high:
        mid = (low + high) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return low
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int searchInsert(vector<int>& nums, int target) {
    int low = 0, high = nums.size() - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return low;
}
```
</details>

> ⏱️ Time O(log n) · Space O(1)

---

## Solution 3 — First and Last Position of Element

> **Idea:** Run binary search **twice** — once biased to keep going *left* (first occurrence), once biased *right* (last occurrence).

<details>
<summary>☕ Java</summary>

```java
int[] searchRange(int[] nums, int target) {
    int first = findBound(nums, target, true);
    int last  = findBound(nums, target, false);
    return new int[]{first, last};
}
int findBound(int[] nums, int target, boolean isFirst) {
    int low = 0, high = nums.length - 1, result = -1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (nums[mid] == target) {
            result = mid;
            if (isFirst) high = mid - 1;   // keep looking left
            else low = mid + 1;            // keep looking right
        } else if (nums[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return result;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def search_range(nums, target):
    def find_bound(is_first):
        low, high, result = 0, len(nums) - 1, -1
        while low <= high:
            mid = (low + high) // 2
            if nums[mid] == target:
                result = mid
                if is_first:
                    high = mid - 1      # keep looking left
                else:
                    low = mid + 1       # keep looking right
            elif nums[mid] < target:
                low = mid + 1
            else:
                high = mid - 1
        return result
    return [find_bound(True), find_bound(False)]
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int findBound(vector<int>& nums, int target, bool isFirst) {
    int low = 0, high = nums.size() - 1, result = -1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (nums[mid] == target) {
            result = mid;
            if (isFirst) high = mid - 1;   // keep looking left
            else low = mid + 1;            // keep looking right
        } else if (nums[mid] < target) low = mid + 1;
        else high = mid - 1;
    }
    return result;
}
vector<int> searchRange(vector<int>& nums, int target) {
    return {findBound(nums, target, true), findBound(nums, target, false)};
}
```
</details>

> ⏱️ Time O(log n) · Space O(1)

---

## Solution 4 — Floor in a Sorted Array

> **Floor** = the largest element that is ≤ target. When `mid` is ≤ target, record it and search right for something even bigger (but still ≤ target).

<details>
<summary>☕ Java</summary>

```java
int findFloor(int[] arr, int x) {
    int low = 0, high = arr.length - 1, ans = -1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] <= x) {
            ans = mid;          // candidate floor
            low = mid + 1;      // try to find a bigger valid one
        } else high = mid - 1;
    }
    return ans;                 // index of floor (-1 if none)
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def find_floor(arr, x):
    low, high, ans = 0, len(arr) - 1, -1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] <= x:
            ans = mid           # candidate floor
            low = mid + 1       # try for a bigger valid one
        else:
            high = mid - 1
    return ans
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int findFloor(vector<int>& arr, int x) {
    int low = 0, high = arr.size() - 1, ans = -1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] <= x) {
            ans = mid;          // candidate floor
            low = mid + 1;      // try for a bigger valid one
        } else high = mid - 1;
    }
    return ans;
}
```
</details>

> ⏱️ Time O(log n) · Space O(1)

---

## Solution 5 — Search in Rotated Sorted Array

> **Idea:** Even after rotation, *one half is always sorted*. Find the sorted half, check if the target lies inside it, and search accordingly.

<details>
<summary>☕ Java</summary>

```java
int search(int[] nums, int target) {
    int low = 0, high = nums.length - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (nums[mid] == target) return mid;
        if (nums[low] <= nums[mid]) {            // left half sorted
            if (nums[low] <= target && target < nums[mid]) high = mid - 1;
            else low = mid + 1;
        } else {                                  // right half sorted
            if (nums[mid] < target && target <= nums[high]) low = mid + 1;
            else high = mid - 1;
        }
    }
    return -1;
}
```
</details>

<details>
<summary>🐍 Python</summary>

```python
def search(nums, target):
    low, high = 0, len(nums) - 1
    while low <= high:
        mid = (low + high) // 2
        if nums[mid] == target:
            return mid
        if nums[low] <= nums[mid]:               # left half sorted
            if nums[low] <= target < nums[mid]:
                high = mid - 1
            else:
                low = mid + 1
        else:                                    # right half sorted
            if nums[mid] < target <= nums[high]:
                low = mid + 1
            else:
                high = mid - 1
    return -1
```
</details>

<details>
<summary>⚡ C++</summary>

```cpp
int search(vector<int>& nums, int target) {
    int low = 0, high = nums.size() - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (nums[mid] == target) return mid;
        if (nums[low] <= nums[mid]) {            // left half sorted
            if (nums[low] <= target && target < nums[mid]) high = mid - 1;
            else low = mid + 1;
        } else {                                  // right half sorted
            if (nums[mid] < target && target <= nums[high]) low = mid + 1;
            else high = mid - 1;
        }
    }
    return -1;
}
```
</details>

> ⏱️ Time O(log n) · Space O(1). This is the "boss level" of binary search — don't worry if it takes a few tries. 💪
