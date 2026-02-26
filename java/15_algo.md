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

```java
public class PrefixSumExample {
    public static int[] buildPrefix(int[] nums) {
        int[] prefix = new int[nums.length+1];
        for (int i = 0; i < nums.length; i++) {
            prefix[i+1] = prefix[i] + nums[i];
        }
        return prefix;
    }

    public static int rangeSum(int[] prefix, int L, int R) {
        return prefix[R+1] - prefix[L];
    }

    public static void main(String[] args) {
        int[] nums = {2, 4, 6, 8};
        int[] prefix = buildPrefix(nums);
        System.out.println(rangeSum(prefix, 1, 3)); // 4+6+8=18
    }
}
```
# 2️⃣ Two Pointers
### 🔹 Idea: Use two indices moving from ends or same side to solve problems efficiently.

✅ Problem: Check if an array has a pair that sums to a target.


```java
import java.util.*;
public class TwoPointersExample {
    public static boolean hasPair(int[] nums, int target) {
        Arrays.sort(nums);
        int left = 0, right = nums.length-1;
        while (left < right) {
            int sum = nums[left] + nums[right];
            if (sum == target) return true;
            if (sum < target) left++;
            else right--;
        }
        return false;
    }

    public static void main(String[] args) {
        int[] nums = {2,7,11,15};
        System.out.println(hasPair(nums, 9)); // true
    }
}

```

# 3️⃣ Sliding Window
### 🔹 Idea: Maintain a subarray/window and slide it to optimize O(N²) problems to O(N).

✅ Problem: Find max sum of subarray of size K.

```java
public class SlidingWindowExample {
    public static int maxSumSubarray(int[] nums, int k) {
        int windowSum = 0;
        for (int i = 0; i < k; i++) windowSum += nums[i];
        int maxSum = windowSum;

        for (int i = k; i < nums.length; i++) {
            windowSum += nums[i] - nums[i-k];
            maxSum = Math.max(maxSum, windowSum);
        }
        return maxSum;
    }

    public static void main(String[] args) {
        int[] nums = {1,4,2,10,23,3,1,0,20};
        System.out.println(maxSumSubarray(nums, 4)); // 39
    }
}

```

# 4️⃣ Fast & Slow Pointers
### 🔹 Idea: Two pointers moving at different speeds to detect cycles or middle nodes.

✅ Problem: Detect cycle in LinkedList.

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}
public class FastSlowExample {
    public static boolean hasCycle(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }
        return false;
    }
}

```

# 5️⃣ LinkedList In-place Reversal
### 🔹 Idea: Reverse a LinkedList without extra space.

✅ Problem: Reverse a LinkedList.

```java
public class ReverseLinkedList {
    public static ListNode reverse(ListNode head) {
        ListNode prev = null, curr = head;
        while (curr != null) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}
```

# 6️⃣ Monotonic Stack
### 🔹 Idea: Stack that maintains increasing or decreasing order to solve span/next-greater problems.

✅ Problem: Next Greater Element.

```java

import java.util.*;
public class MonotonicStackExample {
    public static int[] nextGreater(int[] nums) {
        Stack<Integer> stack = new Stack<>();
        int[] res = new int[nums.length];
        Arrays.fill(res, -1);
        for (int i = 0; i < nums.length; i++) {
            while (!stack.isEmpty() && nums[i] > nums[stack.peek()]) {
                res[stack.pop()] = nums[i];
            }
            stack.push(i);
        }
        return res;
    }
}
```

# 7️⃣ Top K Elements
### 🔹 Idea: Use Min-Heap or Max-Heap to track K largest or smallest elements.

✅ Problem: Find K largest elements.

```java
import java.util.*;
public class TopKExample {
    public static List<Integer> findKLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        for (int num : nums) {
            minHeap.add(num);
            if (minHeap.size() > k) minHeap.poll();
        }
        return new ArrayList<>(minHeap);
    }
}

```

# 8️⃣ Overlapping Intervals
### 🔹 Idea: Sort intervals and merge overlapping ones.

✅ Problem: Merge intervals.

```java
import java.util.*;
public class MergeIntervals {
    public static int[][] merge(int[][] intervals) {
        Arrays.sort(intervals, Comparator.comparingInt(a -> a[0]));
        List<int[]> res = new ArrayList<>();
        int[] current = intervals[0];
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] <= current[1]) {
                current[1] = Math.max(current[1], intervals[i][1]);
            } else {
                res.add(current);
                current = intervals[i];
            }
        }
        res.add(current);
        return res.toArray(new int[res.size()][]);
    }
}

```

# 9️⃣ Modified Binary Search
### 🔹 Idea: Apply binary search in rotated/special arrays.

✅ Problem: Search in rotated sorted array.

```java
public class ModifiedBinarySearch {
    public static int search(int[] nums, int target) {
        int l=0, r=nums.length-1;
        while (l<=r) {
            int mid = (l+r)/2;
            if (nums[mid]==target) return mid;
            if (nums[l]<=nums[mid]) {
                if (target>=nums[l] && target<nums[mid]) r=mid-1;
                else l=mid+1;
            } else {
                if (target>nums[mid] && target<=nums[r]) l=mid+1;
                else r=mid-1;
            }
        }
        return -1;
    }
}
```

# 🔟 Binary Tree Traversal
### 🔹 Idea: Visit nodes in Preorder, Inorder, Postorder.

✅ Problem: Inorder traversal.

```java
import java.util.*;
class TreeNode {
    int val;
    TreeNode left,right;
    TreeNode(int x){val=x;}
}
public class InorderTraversal {
    public static List<Integer> inorder(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        while (curr!=null || !stack.isEmpty()) {
            while (curr!=null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            res.add(curr.val);
            curr = curr.right;
        }
        return res;
    }
}

```

# 1️⃣1️⃣ Depth-First Search (DFS)
### 🔹 Idea: Explore as deep as possible before backtracking.

✅ Problem: Count connected components in graph.

```java
import java.util.*;
public class DFSExample {
    static void dfs(int node, boolean[] visited, List<List<Integer>> graph){
        visited[node]=true;
        for(int nei: graph.get(node)){
            if(!visited[nei]) dfs(nei, visited, graph);
        }
    }
}
```

# 1️⃣2️⃣ Breadth-First Search (BFS)
### 🔹 Idea: Explore level-by-level using queue.

✅ Problem: Shortest path in unweighted graph.

```java
import java.util.*;
public class BFSExample {
    public static void bfs(int start, List<List<Integer>> graph){
        boolean[] visited=new boolean[graph.size()];
        Queue<Integer> q=new LinkedList<>();
        q.add(start); visited[start]=true;
        while(!q.isEmpty()){
            int node=q.poll();
            for(int nei:graph.get(node)){
                if(!visited[nei]){
                    visited[nei]=true;
                    q.add(nei);
                }
            }
        }
    }
}
```

# 1️⃣3️⃣ Matrix Traversal
### 🔹 Idea: Iterate grid in 4 directions, handle bounds.

✅ Problem: Count islands in grid.

```java
public class MatrixTraversal {
    static int rows, cols;
    static void dfs(int[][] grid, int i, int j){
        if(i<0||j<0||i>=rows||j>=cols||grid[i][j]==0) return;
        grid[i][j]=0;
        dfs(grid,i+1,j); dfs(grid,i-1,j); dfs(grid,i,j+1); dfs(grid,i,j-1);
    }
    public static int countIslands(int[][] grid){
        rows=grid.length; cols=grid[0].length;
        int count=0;
        for(int i=0;i<rows;i++){
            for(int j=0;j<cols;j++){
                if(grid[i][j]==1){
                    count++;
                    dfs(grid,i,j);
                }
            }
        }
        return count;
    }
}
```

# 1️⃣4️⃣ Backtracking
### 🔹 Idea: Build solution step-by-step, backtrack when invalid.

✅ Problem: Generate all permutations.

```java
import java.util.*;
public class Permutations {
    public static void permute(int[] nums, List<List<Integer>> res, List<Integer> curr, boolean[] used){
        if(curr.size()==nums.length){
            res.add(new ArrayList<>(curr)); return;
        }
        for(int i=0;i<nums.length;i++){
            if(used[i]) continue;
            used[i]=true; curr.add(nums[i]);
            permute(nums,res,curr,used);
            curr.remove(curr.size()-1); used[i]=false;
        }
    }
}
```

# 1️⃣5️⃣ Dynamic Programming Patterns
### 🔹 Idea: Solve overlapping subproblems using memoization/tabulation.

✅ Problem: Fibonacci using DP.

```java
public class DPExample {
    public static int fib(int n){
        if(n<=1) return n;
        int[] dp = new int[n+1];
        dp[0]=0; dp[1]=1;
        for(int i=2;i<=n;i++) dp[i]=dp[i-1]+dp[i-2];
        return dp[n];
    }
}
```

✅ These 15 patterns cover 90% of algorithm problems.