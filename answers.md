# CMPS 6610 Extra Credit Answers

**Name:** Arjun Dadhwal

  
In this extra credit assignment, we will test and review concepts you
   have learned since the midterm exam. Please add your written answers
   to `answers.md` which you can convert to a PDF using
   `convert.sh`. Alternatively, you may scan and upload written
   answers to a file named `answers.pdf`.

 ________________________________________________________________________________________________________________________________________________________


1. **Algorithmic Paradigms**

My favorite algorithm paradigm would be **Dynamic Programming**.

I really liked its versatility and how the same basic pattern is applicable to so many different types of problems throughout all the modules we studied in the later half of the semester.

What appealed the most was to me the recurring structural pattern:

1. **Optimal substructure**: Expressing and breaking down the problem as a recurrence on optimal solutions to smaller sub-problems, for e.g. OPT(n,W) for the 0-1 Knapsack problem.
2. **Overlapping sub-problems + memoization**: Instead of doing the recursion with same state exponentially many times, the "answers" to these states can be memoized potentially turning an exponential brute force search algorithm into a more efficient polynomial-time one.

I enjoyed writing down the recurrences and identifying the rights because once that is done, the algorithm feels almost like its "self writing": the recursion and memoization follow quite systematically from the formulation.

Dynamic Programming (DP) also looks very simple on the surface, but it captures a lot of complex logic in a very structured way. It also connects quite nicely to the cost models and work span analysis: Not only are these solutions more efficient, but are often easier to reason about and can sometimes even be parallelized by filling the table in a structured way.

 ________________________________________________________________________________________________________________________________________________________


2. **Divide and Conquer**

- No, Divide and Conquer can be used on many problems where there is no notion of any "optimality", so they do not necessary need to have an optimal substructure property.
- Counter example: Sorting (MergeSort / QuckSort)
  -   Problem: Given an array A, output the elements of A in non-decreasing order.
  -   We solve it by divide and conquer
    -   Split A into two halves AL, AR.
    -   Recursively sort AL and AR.
    -   Merge the two sorted halves.
 - This Divide and Conquer algorithm is not an optimization problem since there is exactly one correct sorted output and we are not choosing among may candidate solutions that have different costs. Therefore, a statement like "OPT(A) is built from OPT(Al) and OPT(Ar)" does not make sense since there is no objective function and no better or worse solution. Only "correct" and "incorrect".
 - Divide and Conquer is a structural technique which can be applied to a lot of decision, search, and transfromation problems whereas the optimal substructure is a property of optimization problems.
 - Therefore, problems that are solvable by Divide and Conquer do not necessarily satsify the optimal substructure property.
    ________________________________________________________________________________________________________________________________________________________



3. **Randomization**
- Let X be the random variable: "number of comparisons performed by randomized Quicksort on an input of size n".
- We know that:
  - $\mathbb{E}[X] = O(n \log n)$
- Write this as $\mathbb{E}[X] \leq cn\log n$ for some fixed constant $c > 0$.
- Markov's inequality states that for any $\alpha > 0$
  - $\Pr[X \geq \alpha] \leq \frac{\mathbb{E}[X]}{\alpha}$
 ________________________________________________________________________________________________________________________________________________________
- 3a.
- The probability that Quicksort does $\Omega(n^2)$ comparisons.
- $\Omega(n^2)$ means that at least $kn^2$ comparisons for some constant $k > 0$.
- Setting $\alpha = kn^2$
  - $\Pr[X \geq kn^2] \leq \frac{\mathbb{E}[X]}{kn^2} \leq \frac{cn\log n}{kn^2} = \frac{c}{k} \cdot \frac{\log n}{n} = O\left(\frac{\log n}{n}\right)$
- So the probability that Quicksort takes quadratic times is at most $O\left(\frac{\log n}{n}\right)$ which goes to 0 as n grows.

 ________________________________________________________________________________________________________________________________________________________

- 3b.
- If we set the threshold to $\alpha = 10^c n \ln n$ for some constant $c > 0$:
  - $\Pr[X \geq 10^c n\ln n] \leq \frac{\mathbb{E}[X]}{10^c n\ln n} \leq \frac{cn\ln n}{10^c n\ln n} = \frac{c}{10^c} = O(10^{-c})$.
- So the probability that Quicksort uses $10^c$ times the $Θ(n\log n)$ work is at most on the ordr of $10^{-c}$, it decays exponentially in c but not in n.
- Interpretation:
  - Almost all the probaiblity mass of X is clustered around its expected value $Θ(n\log n)$. The chance that the QuickSort runs much slower than its expectation by a factor liek $10^c$ is very small.

 _________________________________________________________________________________________


4. **Greedy Algorithms**
- Show that the Shortest-Job-First (SJF) paradigm sorts the job by non-decreasing processing time and minimizes the average waiting time.
- **Step 1: Reduce to minimizing total waiting time**
  -   The cost
    -   $C(S) = \frac{1}{n}\sum_{k=1}^{n} w_k$
  -   is just the total waiting time divided by n.
  -   Since n is fixed, minimizing $C(S)$ is the equivalent to minimizing.
    -   $W_{\text{tot}}(S) = \sum_{k=1}^{n} w_k$.
 - **Step 2: Local swap argument (Greedy-choice)**
   - Consider an schedule S.
   - Suppose somewhere in S there are two jobs that appear consecutively in the order:
     - (job A, time a), (job b, time b)
   - with $a > b$
   - Let T be the total processing time of all the jobs scheduled before this paper.
   - So under order A then B:
     - Waiting time of A: $w_A = T$
     - Waiting time of B: $w_B = T + a$
    - Their contribution to the total waiting time is:
      - $w_A + w_B = T + (T + a) = 2T + a$
   - Now consider the swapped order B then A:
     - Waiting time of B: $w'_B = T$
     - Waiting time of A: $w'_A = T + b$
   - Contribution becomes:
     - $w'_A + w'_B = T + (T + b) = 2T + b$
   - Since we assume $a > b$,
     - $2T + b < 2T + a \Rightarrow w'_A + w'_B < w_A + w_B$
   - All other jobs keep the same waiting times, so the total waiting time will strictly decrease when we swap a longer job in front of a shorter one <=> cost $C(S)$ strictly decreases.
   - Therefore, in any optimal schedule there can be no adjacent pair with a longer job before a shorter job.
 - **Step 3: Conclude global order**
   - A schedule with no such inversions is exactly a schedule where the jobs are sorted by non-decreasing processing times, therefore:
     - Starting from any schedule, we can repeatedly swap any inverted pair, the longer before the shorter.
     - Each swap does not increase, but rather decreases the total waiting time.
     - Eventually we will obtain the schedule that is sorted by processing times.
     - Hence, the sorted schedule would have waiting time at most that of any other schedule.
   - Therefore, SJF yields an optimal schedule for minimizing average waiting time.








_________________________________________________________________________________________




5. **Dynamic Programming**

6. **Graphs**
