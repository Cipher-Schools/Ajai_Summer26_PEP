# 🎯 DSA Practice Problem List

> Practice set for students. Solve at your own pace. Each row tells you the core idea so you know *why* you're solving it.

| Problem | Difficulty | Link | Key Idea |
|---------|-----------|------|----------|
| Binary Search | Easy | https://leetcode.com/problems/binary-search/ | The core skeleton — memorize this |
| Search Insert Position | Easy | https://leetcode.com/problems/search-insert-position/ | Where target should go if missing |
| First Bad Version | Easy | https://leetcode.com/problems/first-bad-version/ | Binary search on a boolean condition |
| Find First and Last Position of Element | Medium | https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/ | Two biased searches (left / right bound) |
| Floor in a Sorted Array | Easy | https://www.geeksforgeeks.org/problems/floor-in-a-sorted-array-1587115620/1 | Largest element ≤ target |
| Ceil the Floor | Easy | https://www.geeksforgeeks.org/problems/ceil-the-floor2802/1 | Smallest element ≥ target |
| Number of Occurrences of a Number | Easy | https://www.geeksforgeeks.org/problems/number-of-occurrence2259/1 | Last index − first index + 1 |
| Search in Rotated Sorted Array | Medium | https://leetcode.com/problems/search-in-rotated-sorted-array/ | One half is always sorted — check which |
| Search in Rotated Sorted Array II | Medium | https://leetcode.com/problems/search-in-rotated-sorted-array-ii/ | Same idea + handle duplicates |
| Find Minimum in Rotated Sorted Array | Medium | https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/ | Compare mid to right end to find the break |
| Find Peak Element | Medium | https://leetcode.com/problems/find-peak-element/ | Climb toward the uphill neighbor |
| Peak Index in a Mountain Array | Medium | https://leetcode.com/problems/peak-index-in-a-mountain-array/ | Binary search for the peak |
| Single Element in a Sorted Array | Medium | https://leetcode.com/problems/single-element-in-a-sorted-array/ | Pairs break at the single element |
| Sqrt(x) | Easy | https://leetcode.com/problems/sqrtx/ | Search the ANSWER space, not the array |
| Koko Eating Bananas | Medium | https://leetcode.com/problems/koko-eating-bananas/ | Binary search on eating speed |
| Capacity To Ship Packages Within D Days | Medium | https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/ | Binary search on ship capacity |
| Minimum Number of Days to Make m Bouquets | Medium | https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/ | Binary search on number of days |
| Magnetic Force Between Two Balls | Medium | https://leetcode.com/problems/magnetic-force-between-two-balls/ | Binary search on minimum gap |
| Split Array Largest Sum | Hard | https://leetcode.com/problems/split-array-largest-sum/ | Binary search on the max subarray sum |
| Find the Smallest Divisor Given a Threshold | Medium | https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/ | Binary search on the divisor |
| Aggressive Cows | Medium | https://www.geeksforgeeks.org/problems/aggressive-cows/1 | Binary search on minimum distance |
| Minimize Max Distance to Gas Station | Hard | https://www.geeksforgeeks.org/problems/minimize-max-distance-to-gas-station/1 | Binary search on a decimal answer |
| Reverse String | Easy | https://leetcode.com/problems/reverse-string/ | Two pointers swapping the ends |
| Valid Palindrome | Easy | https://leetcode.com/problems/valid-palindrome/ | Two pointers, skip non-alphanumerics |
| Move Zeroes | Easy | https://leetcode.com/problems/move-zeroes/ | Slow/fast pointer, push non-zeros forward |
| Remove Duplicates from Sorted Array | Easy | https://leetcode.com/problems/remove-duplicates-from-sorted-array/ | Slow pointer marks last unique |
| Squares of a Sorted Array | Easy | https://leetcode.com/problems/squares-of-a-sorted-array/ | Compare both ends, fill answer from the back |
| Two Sum II – Input Array Is Sorted | Medium | https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/ | Classic left/right sum-target pointers |
| 3Sum | Medium | https://leetcode.com/problems/3sum/ | Fix one number, two-pointer the rest |
| 3Sum Closest | Medium | https://leetcode.com/problems/3sum-closest/ | Fix one, two-pointer, track closest sum |
| 4Sum | Medium | https://leetcode.com/problems/4sum/ | Fix two numbers, two-pointer the rest |
| Container With Most Water | Medium | https://leetcode.com/problems/container-with-most-water/ | Move the shorter wall inward |
| Number of Subsequences That Satisfy the Sum Condition | Medium | https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/ | Sort + two pointers + power of 2 counting |
| Contains Duplicate | Easy | https://leetcode.com/problems/contains-duplicate/ | HashSet — seen before? |
| Two Sum | Easy | https://leetcode.com/problems/two-sum/ | HashMap — value → index |
| Valid Anagram | Easy | https://leetcode.com/problems/valid-anagram/ | Frequency array, add & subtract |
| First Unique Character in a String | Easy | https://leetcode.com/problems/first-unique-character-in-a-string/ | Frequency array, 2 passes |
| Find the Difference | Easy | https://leetcode.com/problems/find-the-difference/ | Frequency count / XOR |
| Isomorphic Strings | Medium | https://leetcode.com/problems/isomorphic-strings/ | Two maps, both directions |
| Find Common Characters | Easy | https://leetcode.com/problems/find-common-characters/ | Minimum frequency across words |
| Sort Characters by Frequency | Medium | https://leetcode.com/problems/sort-characters-by-frequency/ | Count + sort by frequency |
| Group Anagrams | Medium | https://leetcode.com/problems/group-anagrams/ | Sorted word as the map key |
| Majority Element | Easy | https://leetcode.com/problems/majority-element/ | Count with a map (or Boyer-Moore) |
| Intersection of Two Arrays | Easy | https://leetcode.com/problems/intersection-of-two-arrays/ | Set intersection |
| Longest Consecutive Sequence | Medium | https://leetcode.com/problems/longest-consecutive-sequence/ | Set lookups to extend runs |
| Subarray Sum Equals K | Medium | https://leetcode.com/problems/subarray-sum-equals-k/ | Prefix sum + hashmap of counts |
| Running Sum of 1D Array | Easy | https://leetcode.com/problems/running-sum-of-1d-array/ | Build the prefix sum |
| Find the Highest Altitude | Easy | https://leetcode.com/problems/find-the-highest-altitude/ | Prefix + track the maximum |
| Find Pivot Index | Easy | https://leetcode.com/problems/find-pivot-index/ | Prefix + balance (left == right) |
| Left and Right Sum Differences | Easy | https://leetcode.com/problems/left-and-right-sum-differences/ | Prefix + difference at each index |
| Minimum Value to Get Positive Step by Step Sum | Easy | https://leetcode.com/problems/minimum-value-to-get-positive-step-by-step-sum/ | Prefix + track the minimum |
| Product of Array Except Self | Medium | https://leetcode.com/problems/product-of-array-except-self/ | Left product × right product |
| Range Sum Query - Immutable | Easy | https://leetcode.com/problems/range-sum-query-immutable/ | Precompute prefix, answer ranges in O(1) |
| Maximum Subarray | Medium | https://leetcode.com/problems/maximum-subarray/ | Running sum, reset when negative (Kadane) |
| Implement Stack Using Array | Easy | https://www.geeksforgeeks.org/problems/implement-stack-using-array/1 | Array + top pointer |
| Implement Stack Using Linked List | Easy | https://www.geeksforgeeks.org/problems/implement-stack-using-linked-list/1 | Push/pop at head |
| Implement Stack Using Queues | Easy | https://leetcode.com/problems/implement-stack-using-queues/ | Pop = transfer n−1, dequeue last |
| Baseball Game | Easy | https://leetcode.com/problems/baseball-game/ | Stack follows operation rules |
| Remove Outermost Parentheses | Easy | https://leetcode.com/problems/remove-outermost-parentheses/ | Counter tracks depth, skip outer |
| Backspace String Compare | Easy | https://leetcode.com/problems/backspace-string-compare/ | '#' = pop, then compare |
| Make The String Great | Easy | https://leetcode.com/problems/make-the-string-great/ | Stack top and curr differ by 32 → pop |
| Remove All Adjacent Duplicates in String | Easy | https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/ | Push if different, pop if same as top |
| Valid Parentheses | Easy | https://leetcode.com/problems/valid-parentheses/ | Push opening, match & pop |
| Minimum Add to Make Parentheses Valid | Medium | https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/ | Count unmatched |
| Minimum Remove to Make Valid Parentheses | Medium | https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/ | Push indices, remove unmatched |
| Longest Valid Parentheses | Hard | https://leetcode.com/problems/longest-valid-parentheses/ | Stack of indices, track distance |
| Next Greater Element | Medium | https://www.geeksforgeeks.org/problems/next-larger-element-1587115620/1 | Stack keeps decreasing order |
| Next Greater Element I | Easy | https://leetcode.com/problems/next-greater-element-i/ | Monotonic stack + hashmap |
| Next Greater Element II | Medium | https://leetcode.com/problems/next-greater-element-ii/ | Circular → traverse 2× |
| Daily Temperatures | Medium | https://leetcode.com/problems/daily-temperatures/ | Stack of indices, pop when warmer |
| Online Stock Span | Medium | https://leetcode.com/problems/online-stock-span/ | Stack of (price, span) pairs |
