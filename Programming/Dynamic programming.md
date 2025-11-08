---
lesson: https://leetcode.com/explore/learn/card/dynamic-programming
---
# What is Dynamic programming
**Dynamic Programming** (DP) is a programming paradigm that can systematically and efficiently explore all possible solutions to a problem. As such, it is capable of solving a wide variety of problems that often have the following characteristics:

1. The problem can be broken down into "*overlapping subproblems*" - smaller versions of the original problem that are re-used multiple times.
2. The problem has an "*optimal substructure*" - an optimal solution can be formed from optimal solutions to the overlapping subproblems of the original problem.
# Bottom-up and Top-down
## Bottom-up
```python
def bottom_up_dp(n):
	map = {}
	map[0] = 0
	map[1]= 1
	
	if n >= 2:
		for i in range(2,n+1):
			map[i] = map[i-1] + map[i-2]
	
	return map[n]
```
## Top-down
```python
def top_down_dp(n):
	memo = {}
	for i in range(n+1):
		if i == 0 or i == 1:
			memo[i] = i
		else:
			memo[i] = memo[i-1] + memo[i-2]

return memo[n]
```
# When to use DP
**The first characteristic** that is common in DP problems is that the problem will ask for the optimum value (maximum or minimum) of something, or the number of ways there are to do something. For example:

- What is the minimum cost of doing...
- What is the maximum profit from...
- How many ways are there to do...
- What is the longest possible...
- Is it possible to reach a certain point...

> [!NOTE]
>  Not all DP problems follow this format, and not all problems that follow these formats should be solved using DP. However, these formats are very common for DP problems and are generally a hint that you should consider using dynamic programming.

**The second characteristic** that is common in DP problems is that future "decisions" depend on earlier decisions. Deciding to do something at one step may affect the ability to do something in a later step. This characteristic is what makes a greedy algorithm invalid for a DP problem - we need to factor in results from previous decisions.
