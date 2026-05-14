# The Torchbearer

**Student Name:** Noah Vargas
**Student ID:** 131028726
**Course:** CS 460 – Algorithms | Spring 2026

> This README is your project documentation. Write it the way a developer would document
> their design decisions , bullet points, brief justifications, and concrete examples where
> required. You are not writing an essay. You are explaining what you built and why you built
> it that way. Delete all blockquotes like this one before submitting.

---

## Part 1: Problem Analysis

> Document why this problem is not just a shortest-path problem. Three bullet points, one
> per question. Each bullet should be 1-2 sentences max.

- **Why a single shortest-path run from S is not enough:**
  _Because we need to travel between relics, not just from S to everywhere._

- **What decision remains after all inter-location costs are known:**
  _What order to visit the relics._

- **Why this requires a search over orders (one sentence):**
  _Since there's many different orders, the cheapest indiv. steps dont always get the cheapest overall path._

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

> List the source node types as a bullet list. For each, one-line reason.

| Source Node Type | Why it is a source |
|---|---|
| _Entrance (S)_ | _find the cheapest starting path to the first relic_ |
| _Relic Chambers (M)_ | _find the cheapest paths between relics and from the last relic to the exit_ |

### Part 2b: Distance Storage

> Fill in the table. No prose required.

| Property | Your answer |
|---|---|
| Data structure name | _Nested Dictionary_ |
| What the keys represent | _Source Node and Destination Node_ |
| What the values represent | _Min. fuel cost_ |
| Lookup time complexity | _O(1)_ |
| Why O(1) lookup is possible | _Because hash map lookups provide constant time lookups_ |

### Part 2c: Precomputation Complexity

> State the total complexity and show the arithmetic. Two to three lines max.

- **Number of Dijkstra runs:** _k+1_
- **Cost per run:** _O(m log n)_
- **Total complexity:** _O((k+1) m log n)_
- **Justification (one line):** _Run 1 dijkstra for the start node and for each of the k relics to build the distance table_

---

## Part 3: Algorithm Correctness

> Document your understanding of why Dijkstra produces correct distances.
> Bullet points and short sentences throughout. No paragraphs.

### Part 3a: What the Invariant Means

> Two bullets: one for finalized nodes, one for non-finalized nodes.
> Do not copy the invariant text from the spec.

- **For nodes already finalized (in S):**
  _The locations where the engine found the absolute min. fuel cost from the start_

- **For nodes not yet finalized (not in S):**
  _The cheapest known fuel cost discovered only using finalized chambers_

### Part 3b: Why Each Phase Holds

> One to two bullets per phase. Maintenance must mention nonnegative edge weights.

- **Initialization : why the invariant holds before iteration 1:**
  _The source starts w/ 0 cost and all the other rooms are set to infinity. It's correct because nothing is explored yet._

- **Maintenance : why finalizing the min-dist node is always correct:**
  _All corridor costs are nonnegative, by picking the current min makes sure that no other path can loop back and give a cheaper route._

- **Termination : what the invariant guarantees when the algorithm ends:**
  _Every reachable room has been assigned to be true, which is the optimal shortest path distance_

### Part 3c: Why This Matters for the Route Planner

> One sentence connecting correct distances to correct routing decisions.

_If the distances are wrong, it'll make its plan based on fake fuel costs and choose a collection order that isn't the cheapest._

---

## Part 4: Search Design

### Why Greedy Fails

> State the failure mode. Then give a concrete counter-example using specific node names
> or costs (you may use the illustration example from the spec). Three to five bullets.

- **The failure mode:** _Your answer here._
- **Counter-example setup:** _Your answer here._
- **What greedy picks:** _Your answer here._
- **What optimal picks:** _Your answer here._
- **Why greedy loses:** _Your answer here._

### What the Algorithm Must Explore

> One bullet. Must use the word "order."

- _Your answer here._

---

## Part 5: State and Search Space

### Part 5a: State Representation

> Document the three components of your search state as a table.
> Variable names here must match exactly what you use in torchbearer.py.

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | | | |
| Relics already collected | | | |
| Fuel cost so far | | | |

### Part 5b: Data Structure for Visited Relics

> Fill in the table.

| Property | Your answer |
|---|---|
| Data structure chosen | |
| Operation: check if relic already collected | Time complexity: |
| Operation: mark a relic as collected | Time complexity: |
| Operation: unmark a relic (backtrack) | Time complexity: |
| Why this structure fits | |

### Part 5c: Worst-Case Search Space

> Two bullets.

- **Worst-case number of orders considered:** _Your answer (in terms of k)._
- **Why:** _One-line justification._

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

> Three bullets.

- **What is tracked:** _Your answer here._
- **When it is used:** _Your answer here._
- **What it allows the algorithm to skip:** _Your answer here._

### Part 6b: Lower Bound Estimation

> Three bullets.

- **What information is available at the current state:** _Your answer here._
- **What the lower bound accounts for:** _Your answer here._
- **Why it never overestimates:** _Your answer here._

### Part 6c: Pruning Correctness

> One to two bullets. Explain why pruning is safe.

- _Your answer here._

---

## References

> Bullet list. If none beyond lecture notes, write that.

- _Your references here._
