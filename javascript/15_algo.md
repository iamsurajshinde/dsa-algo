# 📑 Index

1. [Prefix Sum](#1️⃣-prefix-sum)  
2. [Two Pointers](#2️⃣-two-pointers)  
3. [Sliding Window](#3️⃣-sliding-window)  
4. [Fast & Slow Pointers](#4️⃣-fast--slow-pointers)  
5. [LinkedList In-place Reversal](#5️⃣-linkedlist-in-place-reversal)  
6. [Monotonic Stack](#6️⃣-monotonic-stack)  
7. [Top K Elements](#7️⃣-top-k-elements)  
8. [Overlapping Intervals](#8️⃣-overlapping-intervals)  
9. [Modified Binary Search](#9️⃣-modified-binary-search)  
10. [Binary Tree Traversal](#🔟-binary-tree-traversal)  
11. [Depth-First Search (DFS)](#1️⃣1️⃣-depth-first-search-dfs)  
12. [Breadth-First Search (BFS)](#1️⃣2️⃣-breadth-first-search-bfs)  
13. [Matrix Traversal](#1️⃣3️⃣-matrix-traversal)  
14. [Backtracking](#1️⃣4️⃣-backtracking)  
15. [Dynamic Programming Patterns](#1️⃣5️⃣-dynamic-programming-patterns)

# 1️⃣ Prefix Sum
### 🔹 Idea: Create an auxiliary array where prefix[i] = sum of elements from 0 to i. Allows O(1) range sum queries.

✅ Problem: Given an array nums and Q queries (L, R), find sum of elements between indices L and R.

```javascript
function buildPrefix(nums) {
    const prefix = new Array(nums.length + 1).fill(0);
    for (let i = 0; i < nums.length; i++) {
        prefix[i + 1] = prefix[i] + nums[i];
    }
    return prefix;
}

function rangeSum(prefix, L, R) {
    return prefix[R + 1] - prefix[L];
}

const nums = [2, 4, 6, 8];
const prefix = buildPrefix(nums);
console.log(rangeSum(prefix, 1, 3)); // 4+6+8=18
```

# 2️⃣ Two Pointers
### 🔹 Idea: Use two indices moving from ends or same side to solve problems efficiently.

✅ Problem: Check if an array has a pair that sums to a target.

```javascript
function hasPair(nums, target) {
    nums.sort((a, b) => a - b);
    let left = 0;
    let right = nums.length - 1;

    while (left < right) {
        const sum = nums[left] + nums[right];
        if (sum === target) return true;
        if (sum < target) left++;
        else right--;
    }
    return false;
}

const nums2 = [2, 7, 11, 15];
console.log(hasPair(nums2, 9)); // true
```

# 3️⃣ Sliding Window
### 🔹 Idea: Maintain a subarray/window and slide it to optimize O(N²) problems to O(N).

✅ Problem: Find max sum of subarray of size K.

```javascript
function maxSumSubarray(nums, k) {
    let windowSum = 0;
    for (let i = 0; i < k; i++) windowSum += nums[i];
    let maxSum = windowSum;

    for (let i = k; i < nums.length; i++) {
        windowSum += nums[i] - nums[i - k];
        maxSum = Math.max(maxSum, windowSum);
    }
    return maxSum;
}

const nums3 = [1, 4, 2, 10, 23, 3, 1, 0, 20];
console.log(maxSumSubarray(nums3, 4)); // 39
```

# 4️⃣ Fast & Slow Pointers
### 🔹 Idea: Two pointers moving at different speeds to detect cycles or middle nodes.

✅ Problem: Detect cycle in LinkedList.

```javascript
class ListNode {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

function hasCycle(head) {
    let slow = head;
    let fast = head;

    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow === fast) return true;
    }
    return false;
}
```

# 5️⃣ LinkedList In-place Reversal
### 🔹 Idea: Reverse a LinkedList without extra space.

✅ Problem: Reverse a LinkedList.

```javascript
function reverse(head) {
    let prev = null;
    let curr = head;

    while (curr !== null) {
        const next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

# 6️⃣ Monotonic Stack
### 🔹 Idea: Stack that maintains increasing or decreasing order to solve span/next-greater problems.

✅ Problem: Next Greater Element.

```javascript
function nextGreater(nums) {
    const stack = [];
    const res = new Array(nums.length).fill(-1);

    for (let i = 0; i < nums.length; i++) {
        while (stack.length > 0 && nums[i] > nums[stack[stack.length - 1]]) {
            res[stack.pop()] = nums[i];
        }
        stack.push(i);
    }
    return res;
}
```

# 7️⃣ Top K Elements
### 🔹 Idea: Use Min-Heap or Max-Heap to track K largest or smallest elements.

✅ Problem: Find K largest elements.

```javascript
function findKLargest(nums, k) {
    const minHeap = [];

    for (const num of nums) {
        minHeap.push(num);
        minHeap.sort((a, b) => a - b);
        if (minHeap.length > k) minHeap.shift();
    }

    return minHeap;
}
```

# 8️⃣ Overlapping Intervals
### 🔹 Idea: Sort intervals and merge overlapping ones.

✅ Problem: Merge intervals.

```javascript
function merge(intervals) {
    intervals.sort((a, b) => a[0] - b[0]);
    const res = [];
    let current = intervals[0];

    for (let i = 1; i < intervals.length; i++) {
        if (intervals[i][0] <= current[1]) {
            current[1] = Math.max(current[1], intervals[i][1]);
        } else {
            res.push(current);
            current = intervals[i];
        }
    }
    res.push(current);
    return res;
}
```

# 9️⃣ Modified Binary Search
### 🔹 Idea: Apply binary search in rotated/special arrays.

✅ Problem: Search in rotated sorted array.

```javascript
function search(nums, target) {
    let l = 0;
    let r = nums.length - 1;

    while (l <= r) {
        const mid = Math.floor((l + r) / 2);
        if (nums[mid] === target) return mid;

        if (nums[l] <= nums[mid]) {
            if (target >= nums[l] && target < nums[mid]) r = mid - 1;
            else l = mid + 1;
        } else {
            if (target > nums[mid] && target <= nums[r]) l = mid + 1;
            else r = mid - 1;
        }
    }
    return -1;
}
```

# 🔟 Binary Tree Traversal
### 🔹 Idea: Visit nodes in Preorder, Inorder, Postorder.

✅ Problem: Inorder traversal.

```javascript
class TreeNode {
    constructor(val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}

function inorder(root) {
    const res = [];
    const stack = [];
    let curr = root;

    while (curr !== null || stack.length > 0) {
        while (curr !== null) {
            stack.push(curr);
            curr = curr.left;
        }
        curr = stack.pop();
        res.push(curr.val);
        curr = curr.right;
    }
    return res;
}
```

# 1️⃣1️⃣ Depth-First Search (DFS)
### 🔹 Idea: Explore as deep as possible before backtracking.

✅ Problem: Count connected components in graph.

```javascript
function dfs(node, visited, graph) {
    visited[node] = true;
    for (const nei of graph[node]) {
        if (!visited[nei]) dfs(nei, visited, graph);
    }
}
```

# 1️⃣2️⃣ Breadth-First Search (BFS)
### 🔹 Idea: Explore level-by-level using queue.

✅ Problem: Shortest path in unweighted graph.

```javascript
function bfs(start, graph) {
    const visited = new Array(graph.length).fill(false);
    const q = [];

    q.push(start);
    visited[start] = true;

    while (q.length > 0) {
        const node = q.shift();
        for (const nei of graph[node]) {
            if (!visited[nei]) {
                visited[nei] = true;
                q.push(nei);
            }
        }
    }
}
```

# 1️⃣3️⃣ Matrix Traversal
### 🔹 Idea: Iterate grid in 4 directions, handle bounds.

✅ Problem: Count islands in grid.

```javascript
function countIslands(grid) {
    const rows = grid.length;
    const cols = grid[0].length;

    function dfs(i, j) {
        if (i < 0 || j < 0 || i >= rows || j >= cols || grid[i][j] === 0) return;
        grid[i][j] = 0;
        dfs(i + 1, j);
        dfs(i - 1, j);
        dfs(i, j + 1);
        dfs(i, j - 1);
    }

    let count = 0;
    for (let i = 0; i < rows; i++) {
        for (let j = 0; j < cols; j++) {
            if (grid[i][j] === 1) {
                count++;
                dfs(i, j);
            }
        }
    }
    return count;
}
```

# 1️⃣4️⃣ Backtracking
### 🔹 Idea: Build solution step-by-step, backtrack when invalid.

✅ Problem: Generate all permutations.

```javascript
function permute(nums) {
    const res = [];
    const used = new Array(nums.length).fill(false);

    function backtrack(curr) {
        if (curr.length === nums.length) {
            res.push([...curr]);
            return;
        }
        for (let i = 0; i < nums.length; i++) {
            if (used[i]) continue;
            used[i] = true;
            curr.push(nums[i]);
            backtrack(curr);
            curr.pop();
            used[i] = false;
        }
    }

    backtrack([]);
    return res;
}
```

# 1️⃣5️⃣ Dynamic Programming Patterns
### 🔹 Idea: Solve overlapping subproblems using memoization/tabulation.

✅ Problem: Fibonacci using DP.

```javascript
function fib(n) {
    if (n <= 1) return n;
    const dp = new Array(n + 1).fill(0);
    dp[1] = 1;
    for (let i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
```

✅ These 15 patterns cover 90% of algorithm problems.