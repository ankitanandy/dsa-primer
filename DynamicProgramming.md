# Dynamic Programming (DP)

## Overview
Dynamic Programming is an optimization technique that solves problems by breaking them down into overlapping subproblems and storing the results of subproblems to avoid redundant computations.

## Key Concepts of DP
- **Optimal Substructure**: A problem exhibits optimal substructure if its optimal solution can be constructed from the optimal solutions of its subproblems.
- **Overlapping Subproblems**: A problem has overlapping subproblems if the same subproblem is solved multiple times.

## Steps to Solve a DP Problem
1. **Identify the Subproblem**: Find how the larger problem can be broken down into smaller subproblems.
2. **State Definition**: Define the state clearly (e.g., dp[i] represents the minimum cost to reach step i).
3. **State Transition**: Determine the recurrence relation (e.g., dp[i] = min(dp[i - 1] + cost, dp[i - 2] + cost)).
4. **Base Case**: Define the base cases to initialize the DP array/matrix.
5. **Iterative/Recursive Calculation**: Use bottom-up iteration or top-down recursion with memoization.

## DP Time Complexities
Most DP problems have time complexities proportional to the number of states and the cost of computing each state.

| Type                      | Time Complexity |
|---------------------------|-----------------|
| 1D Array DP               | O(N)            |
| 2D Grid DP                | O(M * N)        |
| Matrix Chain Multiplication | O(N^3)         |

## Types of Dynamic Programming
1. **1D DP (Linear Problems)**
   - Problems that involve one-dimensional states (e.g., dp[i]).
   - Examples: Fibonacci numbers, Climbing Stairs, House Robber.

2. **2D DP (Grid or Matrix Problems)**
   - Problems involving 2D grids or matrices (e.g., dp[i][j]).
   - Examples: Longest Common Subsequence, Edit Distance, Knapsack.

3. **State-Based DP**
   - State transitions involve multiple factors or constraints.
   - Examples: Stock Buy and Sell, Maximum Profit with Cooldown.

4. **Bitmask DP**
   - Used for problems with multiple choices or subsets.
   - Example: Traveling Salesman Problem (TSP).

## Common Dynamic Programming Problems

### 1. Climbing Stairs
**Problem**: Find the number of distinct ways to reach the top of a staircase with N steps.
**State**: dp[i] represents the number of ways to reach step i.
**Transition**: dp[i] = dp[i - 1] + dp[i - 2].
**Time Complexity**: O(N)

### 2. House Robber
**Problem**: Find the maximum money that can be robbed without robbing adjacent houses.
**State**: dp[i] represents the maximum money that can be robbed up to house i.
**Transition**: dp[i] = max(dp[i - 1], dp[i - 2] + nums[i]).
**Time Complexity**: O(N)

### 3. Longest Common Subsequence (LCS)
**Problem**: Find the length of the longest common subsequence between two strings.
**State**: dp[i][j] represents the LCS length of the first i characters of string A and the first j characters of string B.
**Transition**:
- If A[i - 1] == B[j - 1]: dp[i][j] = dp[i - 1][j - 1] + 1.
- Else: dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]).
**Time Complexity**: O(M * N)

### 4. Knapsack (0/1 Knapsack)
**Problem**: Maximize the total value of items that can be put in a knapsack of capacity W.
**State**: dp[i][w] represents the maximum value achievable with the first i items and a weight limit of w.
**Transition**:
- If we exclude item i: dp[i][w] = dp[i - 1][w].
- If we include item i: dp[i][w] = dp[i - 1][w - weight[i]] + value[i].
**Time Complexity**: O(N * W)

### 5. Edit Distance (Levenshtein Distance)
**Problem**: Find the minimum number of operations to convert one string to another.
**State**: dp[i][j] represents the minimum edit distance to convert the first i characters of word1 to the first j characters of word2.
**Transition**:
- If word1[i - 1] == word2[j - 1]: dp[i][j] = dp[i - 1][j - 1].
- Else: dp[i][j] = 1 + min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]).
**Time Complexity**: O(M * N)

## Tricks to Identify Dynamic Programming Problems
1. **Overlapping Subproblems**: If the same subproblem is being solved repeatedly, it’s a sign of DP.
   - Example: Fibonacci numbers (recomputing the same subproblem multiple times).
2. **Optimal Substructure**: If solving the problem for smaller subproblems helps solve the larger problem.
   - Example: Longest Common Subsequence.
3. **Decision-Making Problems**: If the problem involves making choices (e.g., include or exclude an item).
   - Example: 0/1 Knapsack.
4. **Grid Problems**: Problems involving 2D grids with constraints often use 2D DP.
   - Example: Minimum Path Sum in a grid.
5. **"Number of Ways" or "Minimum Cost" Problems**: These phrases often indicate DP.
   - Example: Climbing stairs, coin change problems.

## Optimization Tricks
- **Space Optimization**: Instead of storing all states, store only the previous row or column if possible.
  - Example: Reduce O(N^2) space to O(N) for LCS.
- **Memoization (Top-Down)**: Store results of subproblems in a hash map or array to avoid recomputation.
- **Iterative Bottom-Up Approach**: Build solutions from base cases to the final solution iteratively.

## Sample Notes for DP Problems
- **Definition**: DP solves problems by breaking them into smaller overlapping subproblems and storing their results.
- **Key Steps**:
  - Identify the subproblem.
  - Define the state (dp[i]).
  - Determine the state transition.
  - Initialize base cases.
  - Solve iteratively or recursively.
- **Tricks**: Look for overlapping subproblems, optimal substructure, decision-making, or grid-based constraints.
