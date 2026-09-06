# Primary Project Cards

Projects are divided initially like this: Group 1 gets Project 1, Group 2 gets Project 2, and so on.

**Dataset note:** The course provides the main artificial Edge-LMS dataset. In each card, “Artificial data” describes the patterns the supplied data should contain. Students may optionally generate a documented variant with the provided script, but they do not need to create the complete dataset themselves.

## Project 1 — Students at Risk of Not Completing the Course

**Problem**
A teacher would like to identify students whose course progress appears to be stopping, early enough that support could still be useful.

**Main question**
Can earlier learning activity be used to predict whether a student will complete the course?

**Useful data**

* earlier quiz attempts and scores
* completed tasks
* activity recency and frequency
* attendance or course participation
* course/module progress

**Artificial data**
Create students with different activity and progression patterns. Define a clear rule for what counts as course completion.

**Your task**

* define when the prediction is made;
* construct features using only earlier data;
* create a completion target;
* build and compare suitable predictive models;
* evaluate errors and usefulness.

**Important issue**
Do not use information created after the prediction point. This would cause **data leakage**.

**Extension**
Compare predictions made early, midway and later in the course.

---

## Project 2 — Predict Final Course Performance

**Problem**
Teachers may want to understand how much early-course information tells us about later performance.

**Main question**
How accurately can final performance be predicted from the earlier part of the course?

**Useful data**

* earlier quiz scores
* attempts
* submissions
* course activity
* concept-coverage or task metrics

Edge-LMS currently stores quiz results, task grades and several derived task measurements that can support this type of dataset. 

**Artificial data**
Create different levels of student performance, activity and variability. Include some students whose later results differ from their early results.

**Your task**

* choose a prediction cutoff;
* define final performance;
* construct the analytical dataset;
* compare suitable prediction approaches;
* visualize and interpret prediction errors.

**Important issue**
Later scores and other post-cutoff information must not appear among the features.

**Extension**
Compare a model using scores only with one using activity information as well.

---

## Project 3 — Learning-Behaviour Profiles

**Problem**
Students may work through a course in different ways even when their final results are similar.

**Main question**
Can meaningful patterns of learning behaviour be identified from LMS data?

**Useful data**

* number of quiz attempts
* submission activity
* course activity frequency
* study regularity
* scores
* inactivity periods
* attendance/activity measures

**Artificial data**
Generate several overlapping behaviour patterns, but do not directly store a student “type” in the analytical dataset.

**Your task**

* construct meaningful behavioural variables;
* scale or transform them when necessary;
* identify groups in the data;
* visualize the groups;
* interpret whether they represent meaningful differences.

**Important issue**
Clusters are mathematical groupings. Do not present them as permanent types of student.

**Extension**
Test how stable the groups remain when different variables are included.

---

## Project 4 — Success on the Next Quiz Attempt

**Problem**
Quiz history may contain information about whether the next attempt will be successful.

**Main question**
Can previous quiz activity predict success on a student's next attempt?

**Useful data**

* previous score
* number of previous attempts
* previous item results
* time between attempts
* earlier quiz performance

Edge-LMS records quiz start/submission information, scores, answers, question results and attempt-related information, although raw quiz logs require cleaning and deduplication.  

**Artificial data**
Generate different question difficulties, student performance levels and improvement between attempts.

**Your task**

* define what counts as success;
* construct one observation per prediction;
* use only information available before that attempt;
* compare predictive models;
* analyse incorrect predictions.

**Important issue**
Repeated attempts from the same student are not independent observations.

**Extension**
Predict the probability of success rather than only success/failure.

---

## Project 5 — Quiz Question Difficulty

**Problem**
Teachers need to know which questions are easy, difficult or unexpectedly challenging.

**Main question**
Can the difficulty of a quiz question be estimated from student response data?

**Useful data**

* number of responses
* item scores
* correct/incorrect responses
* attempts
* overall student performance
* question characteristics

**Artificial data**
Create questions with different underlying difficulty levels and students with different performance levels.

**Your task**

* define a numerical measure of question difficulty;
* aggregate response data appropriately;
* investigate factors associated with difficulty;
* estimate question difficulty;
* compare estimates with the known synthetic difficulty.

**Important issue**
Do not use live assessment questions or answer keys in the teaching dataset. Synthetic or retired item identifiers should be used. 

**Extension**
Study whether question difficulty differs between stronger and weaker students.

---

## Project 6 — Questions That May Need Teacher Review

**Problem**
A difficult question is not necessarily a bad question. However, some unusual response patterns may indicate that a question should be inspected.

**Main question**
Can unusual quiz-question behaviour be detected automatically?

**Possible warning signs**

* exceptionally low success
* unusual answer distributions
* many repeated attempts
* unexpected behaviour among otherwise successful students
* performance very different from similar questions

**Artificial data**
Include mostly normal questions and a small number with deliberately unusual behaviour.

**Your task**

* construct question-level variables;
* define what “unusual” means;
* detect unusual questions;
* visualize the results;
* compare detected cases with the known synthetic cases.

**Important issue**
The system should recommend **teacher review**, not declare that a question is incorrect.

**Extension**
Create several different kinds of problematic question and investigate which are easiest to detect.

---

## Project 7 — Learning Activities Associated with Success

**Problem**
Learning systems contain many observable activities, but not all of them are equally informative.

**Main question**
Which combinations of learning activities are associated with successful outcomes?

**Useful data**

* quiz participation
* task submission
* repeated practice
* attendance/activity
* feedback or announcement interaction
* later learning outcomes

This project fits the course's required **association-analysis** content. 

**Artificial data**
Create several activity patterns and deliberately introduce some associations with outcomes.

**Your task**

* transform activity into suitable categories or transactions;
* discover frequent combinations and association rules;
* evaluate their strength;
* identify useful and misleading associations;
* interpret the findings.

**Important issue**
An association does **not** show that one activity caused another outcome.

**Possible Edge-LMS improvement**
A simple course-event log recording material/module opens would make this project substantially richer. Current Edge-LMS does not maintain a general material-page clickstream. 

---

## Project 8 — Unusual LMS Activity

**Problem**
Some system-use patterns differ substantially from ordinary behaviour and may be worth examining.

**Main question**
Can unusual LMS activity patterns be detected without listing every possible unusual case beforehand?

**Possible unusual cases**

* exceptionally many attempts
* unusually rapid sequences of actions
* very long inactivity followed by intense activity
* unexpected combinations of actions
* duplicate or corrupted records

**Artificial data**
Generate normal behaviour and deliberately insert several different kinds of unusual behaviour.

**Your task**

* construct useful behavioural variables;
* establish what normal behaviour looks like;
* detect unusual observations;
* investigate detected cases;
* compare them with the anomalies intentionally generated.

**Important issue**
An unusual observation is not evidence of cheating or misconduct.

**Extension**
Compare detection of individual unusual events with detection of unusual students or periods.

---

## Project 9 — Attempts Needed to Reach Mastery

**Problem**
Different students may require different amounts of practice before demonstrating sufficient understanding.

**Main question**
Can we estimate how many attempts a student will need before reaching a defined mastery level?

**Useful data**

* first-attempt performance
* previous course performance
* question/module difficulty
* earlier attempts
* time between attempts

**Artificial data**
Define a mastery threshold and generate students with different learning rates.

**Your task**

* define mastery;
* determine the number of attempts required;
* construct suitable predictors using earlier information;
* predict the amount of practice required;
* analyse prediction errors.

**Important issue**
Edge-LMS quiz logs can contain several records describing one logical attempt, so raw line counts should not be treated directly as attempt counts. 

**Extension**
Compare prediction separately for easy and difficult course topics.

---

## Project 10 — Difficult Course Modules

**Problem**
Teachers would like to identify parts of a course where students systematically experience difficulties.

**Main question**
Which modules appear to cause the greatest difficulty, and can difficulty be predicted?

**Useful data**

* quiz results by module
* number of attempts
* task results
* concept coverage
* student progression
* inactivity after a module

**Artificial data**
Generate modules with different underlying difficulties and different kinds of difficulty.

**Your task**

* define measurable indicators of module difficulty;
* aggregate student-level data to module level;
* compare modules;
* build a suitable prediction or ranking;
* explain why particular modules appear difficult.

**Important issue**
Low scores alone may not fully represent difficulty.

**Extension**
Distinguish between modules that are conceptually difficult and modules that mainly create workload or data-quality problems.

---

# Reserve Project Cards

## Project 11 — Will an Inactive Student Return?

**Problem**
Periods of inactivity do not necessarily mean that a student has stopped studying permanently.

**Main question**
After a defined period of inactivity, can we predict whether the student will return?

**Useful data**

* previous activity
* previous quiz/submission history
* duration of inactivity
* previous performance
* course progress

**Artificial data**
Generate several patterns: short breaks, recurring gaps and permanent stopping.

**Your task**

* define inactivity;
* define the return period;
* construct observations at the point inactivity is detected;
* build and evaluate a predictive model;
* examine false warnings.

**Important issue**
Current `last_seen` data are an overwritten snapshot rather than a complete activity history. Durable activity logs are also selective. 

**Possible Edge-LMS improvement**
A normalized learning-event history would make this problem easier to study reliably.

---

## Project 12 — Common Learning Paths Through a Course

**Problem**
Students may follow different sequences through course material and learning activities.

**Main question**
Are there common learning paths, and are they associated with different outcomes?

Example paths might resemble:

`material → quiz → material → quiz → next module`

or

`quiz → quiz → material → next module`

**Artificial data**
Generate students following several overlapping learning paths.

**Your task**

* represent activity as sequences;
* identify common sequences or paths;
* compare their frequencies;
* visualize the paths;
* investigate relationships with later outcomes.

**Important issue**
Current Edge-LMS does not record detailed material-page navigation, so this project would rely heavily on synthetic events unless the LMS is extended. 

**Possible Edge-LMS improvement**
Add a minimal event record containing student, timestamp, course/module/resource and event type.

---

## Project 13 — What Happens When Data Quality Becomes Poor?

**Problem**
Machine learning depends on the quality of its input data.

**Main question**
How do different data-quality problems affect machine-learning results?

**Artificial data**
Start with a dataset whose underlying relationships are known. Create controlled versions containing:

* missing values,
* incorrect values,
* duplicates,
* outliers,
* noisy labels,
* class imbalance.

**Your task**

* establish performance on reasonably clean data;
* introduce data problems systematically;
* measure their effect;
* apply appropriate preprocessing;
* measure how much performance can be recovered.

**Important issue**
Different missing values can have different causes. “Feature not recorded” and “student performed no action” should not automatically be treated as the same thing. 

**Extension**
Determine which data-quality problem damages the chosen model most strongly.

---

## Project 14 — Patterns in Written Learning Reflections

**Problem**
Written learning reflections contain text rather than ordinary numerical variables.

**Main question**
Can useful patterns or categories be identified from short learning-related texts?

**Data**
Use **synthetic learning reflections**, not classmates' actual reflections.

Possible synthetic texts could represent different topics, concepts, levels of detail or intentionally defined categories.

**Your task**

* prepare the text for analysis;
* represent text in a form suitable for machine learning;
* investigate patterns or predict a defined synthetic category;
* evaluate the result;
* inspect examples where the method succeeds or fails.

This directly supports the course requirement concerning **machine learning and natural language processing**.  Edge-LMS already contains text submissions and derived text measures, but real free text can contain highly sensitive personal information, so synthetic text is the appropriate default.  

**Important issue**
Do not interpret writing style as evidence of intelligence, personality, mental state or other personal characteristics.

**Extension**
Compare models using only automatically calculated text measures with models using information extracted directly from the synthetic text.

---
