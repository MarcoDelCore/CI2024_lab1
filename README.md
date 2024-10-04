# CI2024_lab1
This solution uses a **Hill Climbing** algorithm to iteratively improve a candidate solution by making small changes (or "tweaks") and accepting changes that lead to a lower cost while maintaining validity. Both the hill climber and the fitness function were adapted from a structure used during class from the professor. 

1. **Initial Solution**: The algorithm starts with a solution that includes all sets, ensuring that the universe is fully covered from the beginning. This approach was chosen because starting from an invalid solution led to continuous invalid solutions during the hill climbing process.
   
2. **Tweak Function**: A random mutation is applied to the current solution by flipping the inclusion of one or more sets. This is controlled by a probability threshold to allow for multiple changes at once.

3. **Fitness Function**: 
   - The fitness function evaluates both the validity and the cost of the solution. I modified this function following the professor’s lecture on the Set Cover problem. The validity (`True` or `False`) is prioritized during the comparison of solutions. Once a valid solution is found, the algorithm focuses on minimizing the cost.

4. **Cost Calculation**: The cost is calculated based on the number of sets selected and their "weight" in covering the universe. The goal is to minimize this cost.

### Execution Flow
- The solution begins with all sets included, ensuring validity.
- In each iteration, the algorithm tweaks the current solution and compares it to the previous one.
- If the new solution is valid and has a lower cost, it is accepted as the new current solution.
- This process is repeated for a predefined number of steps (10,000 in this implementation).

## Code Explanation

- `valid(solution)`: Checks if the current solution covers all elements of the universe.
- `cost(solution)`: Computes the total cost of the current solution.
- `tweak(solution)`: Modifies the current solution by flipping the inclusion of sets.
- `fitness(solution)`: Returns a tuple `(validity, -cost)`, where validity ensures that valid solutions are prioritized during the search.
- The hill climber iteratively tweaks the solution and selects improvements.