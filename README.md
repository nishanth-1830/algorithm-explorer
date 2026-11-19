# Algorithm Explorer: Smart Cargo Packing

A small web app that solves **one real-world problem with four different algorithms**, so you can compare how each one works, how fast it is, and whether its answer is the best possible.

**Live demo:** `https://<your-username>.github.io/algorithm-explorer/`
**Source code:** `https://github.com/<your-username>/algorithm-explorer`

---

## The Problem: 0/1 Knapsack

A delivery truck can carry only a fixed weight (its **capacity**). Each parcel has a **weight** and a **value**. Every parcel is either taken whole or left behind.

**Goal:** choose the parcels that give the highest total value without going over the capacity.

### Why it matters in real life
Courier companies, airlines, shipping lines, and investors all need to get the most value out of limited space, weight, or budget.

### What the program computes
- The best set of parcels to load
- Their total value and total weight
- How many operations each algorithm needed and how long it took
- Whether each algorithm's answer is optimal

---

## Features
- Input form with capacity and a dynamic list of parcels (add and remove rows)
- Input validation with clear error messages
- Four tabs, one per algorithm, each showing:
  - a step-by-step plain-text explanation
  - time and space complexity
  - the result for the user's input
- Side-by-side comparison table of all four approaches
- Responsive layout with automatic light and dark theme

---

## The Four Approaches

| Approach | Idea | Time | Space | Always optimal? |
|---|---|---|---|---|
| **Brute Force** | Try all 2ⁿ combinations and keep the best valid one | O(2ⁿ · n) | O(n) | Yes |
| **Greedy** | Sort by value/weight ratio and take what fits | O(n log n) | O(n) | No |
| **Dynamic Programming** | Build a table of best values for smaller sub-problems | O(n · W) | O(n · W) | Yes |
| **Backtracking + Pruning** | Explore take/skip choices and cut paths that can't win | O(2ⁿ) worst case | O(n) | Yes |

*n = number of parcels, W = truck capacity.*

### How each one works (short version)
1. **Brute force:** every binary number from 0 to 2ⁿ−1 represents one combination, where bit *i* = "take parcel *i*". Check the weight, compute the value, and remember the best.
2. **Greedy:** compute value ÷ weight for each parcel, sort from best to worst, and load each parcel that still fits. It never reconsiders a choice.
3. **Dynamic programming:** `t[i][w]` is the best value using the first *i* parcels with capacity *w*. Each cell is the better of "skip parcel *i*" or "take parcel *i* + best of the remaining capacity". Walk back through the table to recover the chosen parcels.
4. **Backtracking:** recursively try "take" and then "skip". Abandon a path if it exceeds the capacity or if its optimistic estimate can't beat the best answer found so far (pruning).

---

## Input Rules (Validation)

| Field | Rule |
|---|---|
| Capacity | Whole number, 1 to 10,000 |
| Parcel name | Must not be empty |
| Weight | Whole number greater than 0 |
| Value | Whole number, 0 or more |
| Number of parcels | At least 1, at most 20 (keeps brute force fast) |

If anything is invalid, a red message lists every problem.

---

## Try This Example (Greedy Fails)

Set the capacity to **50** and use only these three parcels:

| Parcel | Weight | Value |
|---|---|---|
| A | 10 | 60 |
| B | 20 | 100 |
| C | 30 | 120 |

| Approach | Parcels chosen | Total value |
|---|---|---|
| Greedy | A + B | 160 |
| Brute Force / DP / Backtracking | B + C | **220** |

Greedy picks A first because it has the best ratio, and that blocks the better B + C combination.

---

## Project Structure

```
algorithm-explorer/
├── index.html   # page, styles and all algorithm code (single file)
└── README.md
```

## Run Locally
1. Download or clone the repository.
2. Double-click `index.html`. No installation or build step is needed.

## Deploy (GitHub Pages)
1. Push `index.html` to a public GitHub repository.
2. Go to **Settings → Pages**.
3. Choose **Deploy from a branch**, select `main` and `/(root)`, then click **Save**.
4. After 1–2 minutes the site is live at `https://<your-username>.github.io/<repo-name>/`.

## Tech Stack
HTML5, CSS3, and vanilla JavaScript. No frameworks or libraries.

## Code Map (where to look)
| Part | Location in `index.html` |
|---|---|
| Algorithm explanations and complexities | `INFO` object |
| Brute force | `brute()` |
| Greedy | `greedy()` |
| Dynamic programming | `dp()` |
| Backtracking with pruning | `back()` with helpers `bound()` and `go()` |
| Input validation | `readAndValidate()` |
| Running all algorithms and timing them | `solve()` |
| Tabs and result display | `renderTabs()`, `show()`, `renderCompare()` |

## Team
| Name | Part explained |
|---|---|
| Member 1 | Brute Force |
| Member 2 | Greedy |
| Member 3 | Dynamic Programming |
| Member 4 | Backtracking + Validation |

## License
For educational use.
