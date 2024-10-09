# CI2024_lab1
This solution implements two optimization algorithms, **Hill Climbing** and **Simulated Annealing**, to iteratively improve a candidate solution for a set cover problem. The functions were adapted from a structure introduced by the professor during class. The hill climber's functionality was extended with dynamic mutation control, and a simulated annealing approach was later developed to allow more exploration of the solution space.

## Basic Hill Climber

- **Initial Solution**: The algorithm starts with a solution that includes all sets, ensuring that the universe is fully covered from the outset. This was necessary because, in the basic version, starting from an invalid solution led to continuous invalid solutions, and the hill climber couldn't escape from invalidity. 

- **Tweak Function**: A random mutation is applied to the current solution by flipping the inclusion of one or more sets. This process is governed by a probability threshold that allows for multiple changes, helping to explore the solution space.

### Execution Flow
- The algorithm begins with all sets included, ensuring the initial solution is valid.
- Each iteration applies a mutation to the current solution and evaluates the fitness.
- If the new solution is valid and has a lower cost, it replaces the current one.
- The process repeats over 10,000 steps.

## Improved Hill Climber

In the improved version, several enhancements were made to the algorithm, especially in how it handles starting points and adapts mutation strength dynamically:

- **Starting from an Invalid Solution**: Unlike the basic version, the improved hill climber can begin with a completely random, possibly invalid solution. This flexibility is critical in broadening the search space and avoiding dependency on an initial valid solution. The algorithm uses mutations and adaptive strength control to eventually reach a valid solution.

- **Tweak Function with Adjustable Strength**: 
   - The improved version introduces a tweak function with a parameter for mutation strength, which controls how many sets are randomly included or excluded. 
   - The strength dynamically adjusts based on recent progress: if the algorithm consistently improves, the strength increases, allowing for larger changes; if no improvements are seen, the strength decreases, focusing on smaller tweaks.

### Execution Flow
- The algorithm can start from any random solution, valid or not.
- As it iterates, the mutation strength adapts based on a buffer that tracks recent improvements. If more than half of the recent steps are improvements, the mutation strength increases; otherwise, it decreases.
- Even from an invalid starting point, the hill climber will eventually converge on a valid solution and then work to minimize its cost.
- Like the basic version, this process repeats over 10,000 iterations, adjusting as needed.

## Simulated Annealing

The Simulated Annealing algorithm provides an alternative optimization approach by allowing the exploration of worse solutions with a probability that decreases over time, enabling the algorithm to escape local minima more effectively than hill climbing.

- **Tweak Function**: Similar to the hill climber, the tweak function applies a random mutation by flipping the inclusion of one or more sets. The new solution is always accepted if it improves the fitness. However, even if the new solution is worse, it may be accepted probabilistically based on the current temperature.

- **Cooling Schedule**: The key concept in simulated annealing is the temperature, which starts high and gradually cools down. While the temperature is high, the algorithm has a higher chance of accepting worse solutions to encourage exploration. As the temperature decreases, the algorithm becomes more focused on refinement and improving the current solution.

### Execution Flow

- The algorithm starts with a random initial solution, which may be invalid.
- At each step, a mutation is applied to the solution, and the fitness of the new solution is calculated.
   - If the new solution has better fitness, it is accepted immediately.
   - If the new solution is worse, it may still be accepted with a probability proportional to the difference in fitness and the current temperature.
- The temperature starts high (1000 in this case) and cools down gradually using a cooling rate (0.995 per iteration). As the temperature drops, the probability of accepting worse solutions decreases. he temperature will continue to cool until it reaches a minimum threshold, set at 10<sup>-3</sup>, ensuring that the algorithm eventually stabilizes and reduces exploration as it approaches the final stages of the search.
- The algorithm runs for 10,000 iterations, adapting as necessary.

## Summary

- **Hill Climbing**: In both the basic and improved versions, hill climbing relies on iteratively tweaking a valid solution or converging on one through mutations. The improved version introduces more flexibility by allowing the algorithm to start from invalid solutions and dynamically adjusting mutation strength.

- **Simulated Annealing**: Simulated annealing provides a more exploratory approach to optimization by accepting worse solutions probabilistically. This allows the algorithm to escape local minima more effectively, gradually refining the solution as the temperature decreases.

## Algorithm Selection

The choice of optimization technique is based on the size of the universe and the density of the set elements:

- **Hill Climber** is chosen when the universe size is small (<= 1000) and the set density is sparse (<= 0.2). In this scenario, the problem complexity is lower, and the hill climber can efficiently explore and improve the solution space.

- **Simulated Annealing** is selected when the universe size is large (> 1000) and the set density is higher (>= 0.2). The complexity here requires a more robust exploration technique, like simulated annealing, to avoid getting stuck in local minima and explore a wider search space.

- **Improved Hill Climber** is used in all other cases, combining flexibility with dynamic mutation control to explore solutions effectively when the problem lies between the above extremes.

This approach ensures that the most suitable algorithm is used based on problem characteristics, optimizing the performance of the solution across different scenarios.
