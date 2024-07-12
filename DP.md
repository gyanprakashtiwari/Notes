# Steps to solve any DP problem
1. Define a state
2. Transition of states
3. Final subproblem

# Recursive Mindset

1. Level ,Choice , Check and Move
2. 
# How to think of any DP problem
## Questions to ask while thinking of building a solution
1. Are you building a **subarray, subsequence or subset** ? Choose any one of the 3 options
	1. if subset - try sorting the given choices array and think now
2. Is it a **counting** problem or **optimizing** problem ? 
## Different Forms of DP
### Steps of coding a DP(recursive) problem
- pruning
- basecase
- recursion
- return

## Framework
### Steps
1. Look for form of the problem
2. Decide States and Meaning
3. Decide Transitions
4. check time complexity

### Form 1
Steps
- level
- choice
- check
- move
### Form 2
Ending Form : Best we can do ending/starting at level
**Standard problems :** 
- Longest increasing subsequence
- minimum path sum in a grid from (0,0) to (n-1,m-1)

### Form 3
Multi Sequence DP : When you have multiple sequence and you need to match
**Standard problems :**
- Longest common subsequence

### Form 4
LR DP : given a range `[L,R]` best way to cut for the given range
**Standard problems :**
- Rod cutting problem

### Form 5
Game DP : from current config if i can make a move such that the player playing next config loses . then i am always winning 
**Standard problems :**
- Subtraction problem

![[Screenshot from 2024-07-12 08-30-46.png]]
# Problems
- [[Dice Combinations]]
- [[Minimizing Coins]]
- [[Longest Common Substring]]
- 