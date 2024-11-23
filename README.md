# Problem n^2-1 Puzzle
The **n^2-1 puzzle** is a game consisting of a square grid containing numbers from 1 to \( n^2-1 \) and a blank tile represented by 0. The objective is to arrange the numbers in ascending order by moving tiles adjacent to the blank space. To solve this problem, I implemented two pathfinding algorithms: **A-Star** and **Greedy Best-First Search**.

### Specific Objectives
The comparison between the algorithms was carried out considering:
- **Execution time**.
- The **number of steps** needed to reach the solution.
- The **total cost** in terms of actions performed.

---

## Algorithm Description

#### A\*
The A\* algorithm combines two metrics to decide which state to explore next:
- **g(n):** the cumulative cost from the initial node to the current node.
- **h(n):** a heuristic function estimating the cost to reach the goal state.

The sum \( f(n) = g(n) + h(n) \) allows A\* to find the shortest path while ensuring optimality.

#### Greedy Best-First Search
This algorithm uses only the heuristic \( h(n) \) to decide which node to explore, focusing on states that appear closer to the solution. However, it does not guarantee an optimal solution.  
To prevent the algorithm from delving too deep into the search tree, I added a maximum depth limit, which restricts the algorithm from exploring all possible branches.

### Implementations Used
For both algorithms, I used the **Manhattan distance** as the heuristic function. This metric calculates the sum of the horizontal and vertical distances between each tile and its target position.

Additionally, I implemented a mechanism to track previously visited states for both algorithms. This significantly increased efficiency by reducing execution time.

---

## Results
The experiments were conducted first on a 3x3 grid and then on a 4x4 grid, with a random initialization of **100,000 steps**.

### Performance Comparison for a 3x3 Grid

| Algorithm                  | Number of Steps | Total Cost  | Execution Time |
|----------------------------|-----------------|-------------|----------------|
| **A\***                   | 26              | 2,028       | 0s         |
| **Greedy Best-First Search** | 34              | 297         | 0s         |

- **A\*** found an optimal solution (minimum number of steps) but required more time.
- **Greedy Best-First Search** was faster but found a suboptimal solution.

### Performance Comparison for a 4x4 Grid
| Algorithm                  | Number of Steps | Total Cost  | Execution Time  |
|----------------------------|-----------------|-------------|-----------------|
| **A\***                    | 58              | 6,473,212   | 1m 32.7 s       |
| **Greedy Best-First Search** | 154             | 9,561       | 0.1 s           |

- **A\*** found an optimal solution (minimum number of steps) but required significantly higher computational costs.
- **Greedy Best-First Search** quickly converged to a non-optimal solution but with a much lighter computational cost.

---

## Analysis and Discussion

- **A\*** guarantees an optimal solution by using the function \( f(n) = g(n) + h(n) \), but it explores a larger number of states, requiring more time and memory. As the grid size increases, the algorithm's runtime becomes impractical.
- **Greedy Best-First Search** is faster than A\*, but as the grid size grows, the algorithm struggles to find a solution within a reasonable timeframe.

---

## Conclusions
- The **A\*** algorithm is preferable when the optimality of the solution is crucial, but it demands significantly higher computational resources.
- **Greedy Best-First Search** is useful for applications where speed is prioritized, and solution optimality can be sacrificed.
- Possible improvements include:
  - The use of more advanced heuristic functions.
  - Techniques to reduce memory consumption.
