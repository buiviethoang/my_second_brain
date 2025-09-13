2025-09-03 21:55
Status: 
Topic: 
Tags: [[algorithm]]
## Main
Dynamic Programming (DP) is a method for solving problems by breaking them down into smaller overlapping subproblems and storing their results to avoid recomputation.

### 🔑 Steps to Solve a Dynamic Programming Problem

1. **Identify if the problem is suitable for DP**
    
    - **Optimal substructure**: The optimal solution can be built from solutions of subproblems.
        
    - **Overlapping subproblems**: The same subproblems are solved multiple times.
        
    
    ✅ Example: Fibonacci numbers, shortest paths, knapsack, LIS.

2. **Define the state (subproblem)**
    
    - Ask: _"What parameters uniquely define a subproblem?"_
        
    - State should be the **minimum info needed** to solve the problem.
        
    
    ✅ Example:
    
    - Fibonacci: `dp[n]` = nth Fibonacci number.
        
    - Knapsack: `dp[i][w]` = max value using first `i` items with capacity `w`.

3. **Write the recurrence relation (transition)**

- Express the solution of a state in terms of smaller subproblems.
    
- This is the _core logic_ of DP.
    

✅ Example:

- Fibonacci: `dp[n] = dp[n-1] + dp[n-2]`
    
- Knapsack: `dp[i][w] = max(dp[i-1][w], value[i] + dp[i-1][w-weight[i]])`

4. **Decide the base cases**

- What are the smallest subproblems you already know the answer to?  
    ✅ Example:
    
- Fibonacci: `dp[0] = 0, dp[1] = 1`
    
- Knapsack: `dp[0][w] = 0 for all w`

5. **Choose implementation style**

- **Top-down (memoization)**: recursion + cache results.
    
- **Bottom-up (tabulation)**: iterative, build solutions from base cases.

6. **Compute and return the final answer**

- Typically `dp[n]` or `dp[last_state]`.

```java
# Bottom-up
def fib(n):
    if n < 2:
        return n
    dp = [0] * (n+1)
    dp[0], dp[1] = 0, 1
    for i in range(2, n+1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]

print(fib(10))  # 55


def knapsack(W, weights, values, n):
    dp = [[0]*(W+1) for _ in range(n+1)]

    for i in range(1, n+1):
        for w in range(W+1):
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i-1][w],
                               values[i-1] + dp[i-1][w-weights[i-1]])
            else:
                dp[i][w] = dp[i-1][w]
    return dp[n][W]

print(knapsack(50, [10,20,30], [60,100,120], 3))  # 220
```



## References