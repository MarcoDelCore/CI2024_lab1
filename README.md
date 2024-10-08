# CI2024_lab1
This solution implements a **Hill Climbing** algorithm to iteratively improve a candidate solution by making small changes (or "tweaks") and accepting those that lead to a lower cost while maintaining validity. Both the hill climber and the fitness function were adapted from a structure introduced by the professor during class.

Initially, the basic hill climber required starting from a valid solution to ensure progress. However, an improved version was developed later, allowing the algorithm to start from an invalid (even random) solution and eventually converge to a valid one through dynamic mutation control.

## Basic Hill Climber

- **Initial Solution**: The algorithm starts with a solution that includes all sets, ensuring that the universe is fully covered from the outset. This was necessary because, in the basic version, starting from an invalid solution led to continuous invalid solutions, and the hill climber couldn't escape from invalidity. 

- **Tweak Function**: A random mutation is applied to the current solution by flipping the inclusion of one or more sets. This process is governed by a probability threshold that allows for multiple changes, helping to explore the solution space.

### Execution Flow (Basic Version)
- The algorithm begins with all sets included, ensuring the initial solution is valid.
- Each iteration applies a mutation to the current solution and evaluates the fitness.
- If the new solution is valid and has a lower cost, it replaces the current one.
- The process repeats over 10,000 steps, tracking improvements in fitness.

## Improved Hill Climber

In the improved version, several enhancements were made to the algorithm, especially in how it handles starting points and adapts mutation strength dynamically:

- **Starting from an Invalid Solution**: Unlike the basic version, the improved hill climber can begin with a completely random, possibly invalid solution. This flexibility is critical in broadening the search space and avoiding dependency on an initial valid solution. The algorithm uses mutations and adaptive strength control to eventually reach a valid solution.

- **Tweak Function with Adjustable Strength**: 
   - The improved version introduces a tweak function with a parameter for mutation strength, which controls how many sets are randomly included or excluded. 
   - The strength dynamically adjusts based on recent progress: if the algorithm consistently improves, the strength increases, allowing for larger changes; if no improvements are seen, the strength decreases, focusing on smaller tweaks.

### Execution Flow (Improved Version)
- The algorithm can start from any random solution, valid or not.
- As it iterates, the mutation strength adapts based on a buffer that tracks recent improvements. If more than half of the recent steps are improvements, the mutation strength increases; otherwise, it decreases.
- Even from an invalid starting point, the hill climber will eventually converge on a valid solution and then work to minimize its cost.
- Like the basic version, this process repeats over 10,000 iterations, adjusting as needed.

## Code Explanation (Basic and Improved Versions)

- `valid(solution)`: Verifies that the solution covers all elements of the universe.
- `cost(solution)`: Calculates the total cost of the current solution.
- `tweak(solution, strength)`: In the basic version, this randomly flips set inclusions. In the improved version, it includes dynamic control of mutation strength.
- `fitness(solution)`: Returns a tuple `(validity, -cost)`, where validity ensures the algorithm first prioritizes valid solutions.
- The improved hill climber dynamically adjusts mutation strength and is capable of escaping invalid starting points.

In summary, the basic version requires starting from a valid solution and refines it to minimize cost, while the improved version can start from a completely random or invalid solution and still converge on a valid and optimized outcome. This design was influenced by the lecture’s guidance, enabling the algorithm to explore the solution space more flexibly and efficiently.
