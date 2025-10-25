2025-09-25 21:38
Status: 
Topic: 
Tags: [[algorithm]]
## Main
The **sliding window method** is a powerful technique often used to solve problems involving **arrays, strings, or sequences**, especially when you’re asked to find something in a **contiguous subarray/subsequence** (like maximum/minimum, sum, averages, substring patterns, etc.)


It’s popular in algorithm design because it reduces complexity from **O(n·k)** to **O(n)** in many cases.

## 🔑 Core Idea

Instead of recalculating results for every possible window (brute force), we "slide" a fixed-size or variable-size window across the sequence and update the result efficiently.

## Types of Sliding Windows

### 1. **Fixed-size window**

- You are given a window size `k`.
    
- Common problems: maximum sum of size `k`, moving averages, maximum/minimum in each window.
    

**Steps:**

1. Compute result for the first window.
    
2. Slide window by removing the left element and adding the next element.
    
3. Update result efficiently without recomputing the entire window.
    

**Example – Maximum sum of size `k`:**

```java
int maxSum(int[] arr, int k) {
    int n = arr.length;
    int windowSum = 0;
    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    int maxSum = windowSum;

    for (int i = k; i < n; i++) {
        windowSum += arr[i] - arr[i - k]; // slide
        maxSum = Math.max(maxSum, windowSum);
    }
    return maxSum;
}

```

⏱ Complexity: `O(n)`
### 2. **Variable-size window (two pointers technique)**

- Window size changes dynamically based on conditions.
    
- Used for substring/array problems with constraints (like "longest substring with at most k distinct characters").
    

**Steps:**

1. Expand the right pointer to grow the window.
    
2. Shrink from the left when the condition is violated.
    
3. Track the best result as you go.
    

**Example – Smallest subarray with sum ≥ target:**


```java
int minSubArrayLen(int target, int[] nums) {
    int n = nums.length;
    int left = 0, sum = 0, minLen = Integer.MAX_VALUE;

    for (int right = 0; right < n; right++) {
        sum += nums[right];
        while (sum >= target) { // shrink when condition met
            minLen = Math.min(minLen, right - left + 1);
            sum -= nums[left++];
        }
    }
    return minLen == Integer.MAX_VALUE ? 0 : minLen;
}

```

⏱ Complexity: `O(n)`

## 🚀 Common Problems with Sliding Window

- Maximum sum of subarray of size `k`
    
- Longest substring without repeating characters
    
- Minimum window substring
    
- Longest substring with at most `k` distinct characters
    
- Subarray with given sum
    
- Moving averages, etc.



## References