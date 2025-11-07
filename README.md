# CI2025_lab2

## TRAVELLING SALESMAN PROBLEM

This is the problem presentation.

Given a list of cities and their relative distances, find the shortest possible route that visits each city exactly once and returns to the origin city. 

Or, in other words, find the minimum-cost Hamiltonian cycle

## REPOSITORY STRUCTURE

This is the readme, the entry point that explains what is done.

The file *"travelling_salesman_problem_algorithm.ipynb"* is a notebook that contains the code to solve the problem, for all instances. For each problem instance it loads the data and solves the problem.

All the problem instances provided by the teacher reside in the folder *"problems"*.


## SOLVING ALGORITHM

### GREEDY APPROACH

The solution is represented as a vector as long as the number of cities +1, starting and ending with the same number. For instance a possible solution with 3 cities could be *"0 - 1 - 2 - 0"*.

Considering that given a cycle, wherever you start the cost is the same I decided to always start and end with 0.

A solution is valid if it starts and ends with 0 and contains all the values from 1 to (number of cities -1) once.

Another consideration I have made is that a path that includes shorter links should result in a shorter cycle than one that avoids those links.

So I have to look for the cheapest sequence of valid links that will cover the whole cycle.
I'll use a structure to save all links in a structure, order them by cost and add one at a time in the solution only if adding it does not cause creating a premature cycle. 
Once a link is inserted into the solution I remove from the structure all the links starting from the same source or pointing to the same destination and the reverse link.
I stop when all cities are linked.

### EVOLUTIONARY ALGORITHM

I use it to provide 1 individual while all the others are random and I use an evolutionary algorithm to improve it or provide better ones.

The EA will be of type μ+λ.

The parent selection will be done with exponential ranking. p will start with 1.4 and will slowly decrease. The exponential ranking will use fitness=-cost, so the values will be negative but it will work well anyway because we are interested in the relative order.

A recombination will be a cycle crossover. It will be applied with probability prx.
On the offspring, with probability pmx will be applied an insertion mutation, preserving the first and last positions as 0. 

All these parameters will be optimized using an adaptive optimization that follows the 1 out of five principle. Starting with μ0=50, λ0=k0×μ0 with k0=3, prx0=0.8 and pmx0=0.2
In particular, I will update them every 1/10 of total generations in the following way. 
If every 1/10 of total generations the average number of individuals with fitness higher than the previous best is less than 1/5, I have to increase selectivity so increase by 10% μ, k and prx while reducing by 10% pmx, otherwise pmx will be increased by 10% and μ, k and prx will be decreased by 10%.

## RESULTS
Even if the greedy algorithm causes the execution to last about 6 times longer, it lets us reduce the cost more than 20 times for the r1_1000 problem instance, for example. So, according to me, it's worth the time it takes.

The last execution took 26 minutes and these are the results obtained:

| Problem Instance | Cost |
|------------------|------|
| problem_g_10.npy | 1498 |
| problem_g_20.npy | 1756 |
| problem_g_50.npy | 2909 |
| problem_g_100.npy | 4853 |
| problem_g_200.npy | 6807 |
| problem_g_500.npy | 10839 |
| problem_g_1000.npy | 15470 |
| problem_r1_10.npy | 184 |
| problem_r1_20.npy | 369 |
| problem_r1_50.npy | 602 |
| problem_r1_100.npy | 868 |
| problem_r1_200.npy | 1150 |
| problem_r1_500.npy | 1844 |
| problem_r1_1000.npy | 2805 |
| problem_r2_10.npy | -412 |
| problem_r2_20.npy | -816 |
| problem_r2_50.npy | -2154 |
| problem_r2_100.npy | -4689 |
| problem_r2_200.npy | -9550 |
| problem_r2_500.npy | -24430 |
| problem_r2_1000.npy | -49350 |
| test_problem.npy | 2824 |


## FINAL NOTES

Notebook and report (README) were written by Matteo Zito, with the support of OpenAI's GPT-5 model, used only as a programming assistant.

