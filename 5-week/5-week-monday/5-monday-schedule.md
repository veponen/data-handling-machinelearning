### Monday 5 – Association Analysis

| Time            | Activity                                              | What students do                                                                                                                                         |
| --------------- | ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **09:00–09:20** | Start-up and group check                              | Open Week 4 material, association-analysis notebook and concept map. Check what is complete.                                                             |
| **09:20–10:00** | **Association Analysis entry quiz**                   | Complete the readiness quiz.                                                                                                                             |
| **10:00–10:30** | Concept maps + group comparison                       | Compare difficult, important and surprising concepts from Week 4.                                                                                        |
| **10:30–11:00** | Whole-class discussion                                | Bring up questions about transactions, support, confidence, lift, Apriori, thresholds and interpretation.                                                |
| **11:00–12:00** | **Association-rule investigation**                    | Return to the Week 4 practical using `synthetic-association-dataset.csv`. Choose one result or rule that you do not fully understand and investigate it. |
| **12:00–13:00** | Lunch                                                 |                                                                                                                                                          |
| **13:00–13:40** | Association analysis with the larger Edge-LMS dataset | Discuss what could form a transaction and which events/items could meaningfully occur together.                                                          |
| **13:40–14:30** | Group data investigation                              | Build or sketch a transaction representation and identify possible useful associations.                                                                  |
| **14:30–14:45** | Break                                                 |                                                                                                                                                          |
| **14:45–15:30** | Project connection                                    | Decide whether association analysis helps the project. If yes: transaction, items, useful rule, interpretation limits.                                   |
| **15:30–15:50** | Findings and open questions                           | Groups share interesting, misleading or unresolved rules.                                                                                                |
| **15:50–16:00** | Next week                                             | Introduce **Prediction of Numerical Values / Regression** and the next independent study package.                                                        |

### the morning as a soft gate

Students who are ready can move directly from quiz/concept-map discussion into the practical investigation. Students who have not completed the Week 4 notebook can start from:

**Week 4 Study Package → Wednesday: Practical Exercise – Discover Association Rules**

using:

`synthetic-association-dataset.csv`

### The 11:00 investigation task

The structure:

**Question → experiment → evidence → interpretation**

Good investigation choices:

* Why does a rule have high confidence but lift close to 1?
* What happens when minimum support is lowered?
* Why do many new rules appear?
* Why does a seemingly interesting rule have very low support?
* What happens when minimum confidence is increased?
* Which rules disappear if `lift > 1` is required?
* Is a rule strong because the consequent is already very common?
* Does changing the transaction definition change the rules?

The central Monday question is:

> **Is this genuinely interesting association, or just something that looks impressive because of the way the data and thresholds were chosen?**

> What does one transaction represent?
> What exactly are the items?
> How common is the pattern?
> Is confidence high only because the consequent is common?
> What can we conclude — and what can we not conclude?

The Monday rhythm as before: **readiness → discussion → deeper investigation → larger dataset → project work**.
