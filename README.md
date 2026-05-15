# The Torchbearer

**Student Name:** Noah Vargas
**Student ID:** 131028726
**Course:** CS 460 – Algorithms | Spring 2026

---

## Part 1: Problem Analysis

- **Why a single shortest-path run from S is not enough:**
  _Because we need to travel between relics, not just from S to everywhere._

- **What decision remains after all inter-location costs are known:**
  _What order to visit the relics._

- **Why this requires a search over orders (one sentence):**
  _Since there's many different orders, the cheapest indiv. steps dont always get the cheapest overall path._

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

| Source Node Type | Why it is a source |
|---|---|
| _Entrance (S)_ | _find the cheapest starting path to the first relic_ |
| _Relic Chambers (M)_ | _find the cheapest paths between relics and from the last relic to the exit_ |

### Part 2b: Distance Storage

| Property | Your answer |
|---|---|
| Data structure name | _Nested Dictionary_ |
| What the keys represent | _Source Node and Destination Node_ |
| What the values represent | _Min. fuel cost_ |
| Lookup time complexity | _O(1)_ |
| Why O(1) lookup is possible | _Because hash map lookups provide constant time lookups_ |

### Part 2c: Precomputation Complexity

- **Number of Dijkstra runs:** _k+1_
- **Cost per run:** _O(m log n)_
- **Total complexity:** _O((k+1) m log n)_
- **Justification (one line):** _Run 1 dijkstra for the start node and for each of the k relics to build the distance table_

---

## Part 3: Algorithm Correctness

### Part 3a: What the Invariant Means

- **For nodes already finalized (in S):**
  _The locations where the engine found the absolute min. fuel cost from the start_

- **For nodes not yet finalized (not in S):**
  _The cheapest known fuel cost discovered only using finalized chambers_

### Part 3b: Why Each Phase Holds


- **Initialization : why the invariant holds before iteration 1:**
  _The source starts w/ 0 cost and all the other rooms are set to infinity. It's correct because nothing is explored yet._

- **Maintenance : why finalizing the min-dist node is always correct:**
  _All corridor costs are nonnegative, by picking the current min makes sure that no other path can loop back and give a cheaper route._

- **Termination : what the invariant guarantees when the algorithm ends:**
  _Every reachable room has been assigned to be true, which is the optimal shortest path distance_

### Part 3c: Why This Matters for the Route Planner


_If the distances are wrong, it'll make its plan based on fake fuel costs and choose a collection order that isn't the cheapest._

---

## Part 4: Search Design

### Why Greedy Fails

- **The failure mode:** _Proof by counterexample_
- **Counter-example setup:** _Consider this graph._
  + _S: [(B, 1), (C, 5), (D, 5)]_
  + _B: [(C, 1), (D, 10), (T, 1)]_
  + _C: [(B, 10), (D, 1), (T, 100)]_
  + _D: [(B, 1), (C, 10), (T, 100)]_
  + _T: []_
- **What greedy picks:** _S -> B -> C -> D -> T, with total cost of 103_
- **What optimal picks:** _S -> C -> D -> B -> T, with total cost of 8_
- **Why greedy loses:** _Choosing the closest relic immediately forces a path that sacrifices the most efficient exit route, turning a low cost start expensive_

### What the Algorithm Must Explore

- _The algorithm must explore all valid orders in which the relics can be visited and compare their total cost, pruning any order whose partial cost already exceeds the best known complete route._

---

## Part 5: State and Search Space

### Part 5a: State Representation

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | _current_loc_ | _String_ | _The lookup index for the current location in the graph and distance table_ |
| Relics already collected | _relics_remaining_ | _set_ | _Tracks relics visited by the current branch_ |
| Fuel cost so far | _cost_so_far_ | _float_ | _Tracks total cost_ |

### Part 5b: Data Structure for Visited Relics

| Property | Your answer |
|---|---|
| Data structure chosen | _Set_ |
| Operation: check if relic already collected | Time complexity: _O(1)_ |
| Operation: mark a relic as collected | Time complexity: _O(1)_ |
| Operation: unmark a relic (backtrack) | Time complexity: _O(1)_ |
| Why this structure fits | _Because accessing items are constant time which is great for checking and updating_ |

### Part 5c: Worst-Case Search Space

- **Worst-case number of orders considered:** _O(k!) where k represents the total num of relics to be collected._
- **Why:** _If no branches are pruned, its forced to evaluate every possible permutation of relic visits across the entire search tree._

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

- **What is tracked:** _Current cost and the path is takes_
- **When it is used:** _The cost is checked for every recursion and when it completes_
- **What it allows the algorithm to skip:** _Any paths that would give a higher total cost than the current best_

### Part 6b: Lower Bound Estimation

- **What information is available at the current state:** _Traveled cost and nodes that haven't been visited_
- **What the lower bound accounts for:** _The initial pruning which eliminates any branches that are greater than the total cost_
- **Why it never overestimates:** _Because every choice in greedy is made using the smallest available cost_

### Part 6c: Pruning Correctness

- _All edge weights are nonnegative, meaning a path can't become cheaper the more you travel._
- _In the middle of a route, if it already is greater than the cost of a known complete path, it can't be the optimal. Meaning that it can be discarded._

---

## References

- _None beyond lecture notes._
