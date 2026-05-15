# Development Log – The Torchbearer

**Student Name:** Noah Vargas
**Student ID:** 131028726

---

## Entry 1 – [5/12/2026]: Initial Plan

_I'll start out by just implementing Dijkstra's to precompute the distances between the entrance, relic chambers, and the exit. The most difficult part will most likely be the recursive search later on since I need to make sure that the pruning logic discards the expensive paths without missing the global optimum. Lastly to test my work, I'll use the test cases provided to make sure everything works as intended. For today, I'll be doing parts 1 and 2._

---

## Entry 2 – [5/13/2026]: [Part 3]

_I didn't have much time to get what I wanted to get done. Today I just answered the questions in part C and inserted them into dijkstra invariant check function. Tomorrow I plan to finishing the remaining parts and submitting the final._

---

## Entry 3 – [5/14/2026]: [1st half of session]

_For this session, I was hammering out most of the README and code implementations. This had to have been the most time consuming part. I had a bug when I was writing the _explore function which wasn't finding any valid routes. I was editing the remaining relics set during recursion but not restoring it during backtracking._

---

## Entry 4 – [5/14/2026]: Post-Implementation Reflection

_If I had more time I'd add a tighter lower bound estimate for pruning. I'd also like to add more edge case tests. Overall I'm pretty happy with how it turned out, especially with how much I did today._

---

## Final Entry – [5/14/2026]: Time Estimate

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis | _45 minutes_ |
| Part 2: Precomputation Design | _45 minutes_ |
| Part 3: Algorithm Correctness | _20 minutes_ |
| Part 4: Search Design | _45 minutes_ |
| Part 5: State and Search Space | _30 minutes_ |
| Part 6: Pruning | _35 minutes_ |
| Part 7: Implementation | _120 minutes_ |
| README and DEVLOG writing | _60 minutes_|
| **Total** | _6-7 hours_ |
