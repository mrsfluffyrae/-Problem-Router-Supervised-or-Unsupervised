# Problem Router: Supervised or Unsupervised

**Name:** Rachael  |  **Notebook:** `problem_router_simple.ipynb`

## Method
I asked three questions about every problem:
1. **Label:** do we have known correct answers from the past?
2. **Duty:** do we want to predict that answer, or discover patterns?
3. **Output:** is the result a category, number, group, score or rules?

A problem is **supervised** only if a label exists and we want to predict it. Otherwise it is **unsupervised**. I decided this before thinking about any algorithm, to avoid routing by the tool I know best.

## Routing table

| # | Problem | Label | Output | Route |
|---|---------|-------|--------|-------|
| 1 | Predict if a student will pass | Past pass/fail | Category | Supervised |
| 2 | Find study-habit types | None | Groups | Unsupervised |
| 3 | Estimate rent | Past rents | Number | Supervised |
| 4 | Products bought together | None | Rules | Unsupervised |
| 5 | Card fraud | Chargeback results | Category | Supervised |
| 6 | Odd network traffic | None | Score | Unsupervised |
| 7 | Forecast sales | Next month's sales | Number | Supervised |
| 8 | Feedback themes | None | Groups | Unsupervised |
| 9 | Spam filter | User spam clicks | Category | Supervised |
| 10 | Support tickets (ambiguous) | Partial tags | Category | Supervised, checked with clustering |

## Key evidence
- A label must answer the question being asked. In Case 8, star ratings show positive or negative, not themes, so it stays unsupervised.
- A label can come from history. In Case 7 the label is next month's sales, which the past data already contains.
- Rare labels do not change the route. In Case 5 fraud is rare, but confirmed examples exist, so it is supervised.

## Adversarial review
For each case I argued against my own routing and answered the objection (notebook, Task 4). For example, "cluster the students" (Case 1) ignores the pass/fail answers we already have, and "use anomaly detection" (Case 5) ignores confirmed fraud examples.

## Ambiguous case (bonus): support tickets
For supervised: the company has named categories and 8,000 tagged tickets, and new tickets must go to a named team. For unsupervised: only 4% are tagged and the tags may be unreliable. I chose supervised first because clusters are unnamed numbers nobody can route. Clustering is used to check the tags, and I would switch to discovery first if the tags proved unreliable.

## Demonstrations and testing
The supervised demo has known answers and is scored on unseen data (accuracy 0.79). The unsupervised demo has no answers, so a person has to read the group averages and name the groups. Two swapped-in cases (predict cancellations: supervised; group songs without genre tags: unsupervised) are routed correctly with the same three questions.

## Conclusion
The route depends on whether a label exists and whether we want to predict it, not on which tool is familiar.
