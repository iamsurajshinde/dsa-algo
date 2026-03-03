# Algorithm Selection Guide

## Table of Contents
1. [Problem Type Patterns](#problem-type-patterns)
    1. [Minimum / Maximum Value](#1-minimum--maximum-value-not-directly-in-array)
    2. [Subarray / Substring Problems](#2-subarray--substring-problems)
    3. [Find Pair / Triplet / Count](#3-find-pair--triplet--count-of-elements)
    4. [Kth Smallest / Largest](#4-kth-smallest--largest--top-k)
    5. [All Possible Ways](#5-all-possible-ways--combinations--arrangements)
    6. [Overlapping Subproblems](#6-overlapping-subproblems--optimal-result)
    7. [Scheduling / Interval](#7-scheduling--interval--selecting-things)
    8. [Graph / Network](#8-graph--network--connections)
    9. [Shortest Path](#9-shortest-path--minimum-distance)
    10. [Dependency / Ordering](#10-dependency--ordering-problems)
    11. [Fast Range Queries](#11-fast-range-queries)
    12. [Tree Structure](#12-tree-structure-problems)
    13. [Large Constraints](#13-large-constraints-brute-force-too-slow)
    14. [Sorted Array](#14-sorted-array)
    15. [Bit / Subset / Masks](#15-bit--subset--masks)
2. [Interview Quick Reference](#interview-quick-reference)

## Problem Type Patterns

### 1. Minimum / Maximum Value (Not Directly in Array)
**Examples:** minimum days, minimum speed, minimum time, minimum capacity, maximum possible, at least / at most

**Use:** Binary Search on Answer

### 2. Subarray / Substring Problems
**Examples:** longest subarray, shortest subarray, substring with condition, window size problems

**Use:** Sliding Window, Two Pointers

### 3. Find Pair / Triplet / Count of Elements
**Examples:** two sum, count pairs, unique elements, frequency based

**Use:** HashMap / HashSet

### 4. Kth Smallest / Largest / Top K
**Examples:** kth smallest, kth largest, top 10 elements, running median

**Use:** Heap (Priority Queue)

### 5. All Possible Ways / Combinations / Arrangements
**Examples:** all permutations, all subsets, all valid paths, N queens, word search

**Use:** Backtracking

### 6. Overlapping Subproblems + Optimal Result
**Examples:** maximum profit, minimum cost, number of ways, longest sequence, optimal strategy

**Use:** Dynamic Programming

### 7. Scheduling / Interval / Selecting Things
**Examples:** meeting rooms, activity selection, job scheduling, interval overlap

**Use:** Greedy, Sorting + Greedy

### 8. Graph / Network / Connections
**Examples:** number of islands, connected components, shortest path, can we reach, dependency order

**Use:** BFS / DFS

### 9. Shortest Path / Minimum Distance
**Examples:** minimum distance between nodes, cheapest path, shortest route

**Use:** BFS (unweighted), Dijkstra (weighted), Bellman-Ford (negative edges)

### 10. Dependency / Ordering Problems
**Examples:** course schedule, build order, task dependency

**Use:** Topological Sort

### 11. Fast Range Queries
**Examples:** sum in range, update and query, max in range

**Use:** Prefix Sum, Segment Tree, Fenwick Tree

### 12. Tree Structure Problems
**Examples:** LCA, diameter, depth, subtree problems

**Use:** DFS on Tree, Binary Lifting

### 13. Large Constraints (Brute Force Too Slow)
**Examples:** n up to 10⁵ or more, repeated queries

**Use:** Precomputation, Prefix / HashMap / Segment Tree

### 14. Sorted Array
**Examples:** find something, first/last position, closest value

**Use:** Binary Search

### 15. Bit / Subset / Masks
**Examples:** subsets, toggling states, unique number problems

**Use:** Bit Manipulation, Bitmask DP

## Interview Quick Reference

When reading a problem, ask these 5 questions:

| Question | Answer |
|----------|--------|
| **Q1:** Is the answer a number in a range and we must find min / max? | → Binary Search on Answer |
| **Q2:** Are we looking at subarray / substring? | → Sliding Window / Two Pointers |
| **Q3:** Do we need all ways? | → Backtracking |
| **Q4:** Is it optimization with reuse of subproblems? | → Dynamic Programming |
| **Q5:** Is it nodes + edges? | → BFS / DFS |

