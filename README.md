# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

I chose r/investing for my dataset and created five categories: analysis, hot take, reaction, personal experience, and question. While reviewing the posts, I noticed a few patterns in the titles. Some include specific numbers or financial figures, while others make general statements. Some express strong opinions, while others ask questions or share personal experiences. I also found that certain posts focus on individual financial decisions, whereas others discuss broader market trends and company performance. So, I added a separate question and personal_experience categories instead of forcing those posts into another label.
---

## Label Taxonomy

### `analysis`

>**Definition:** A post that examines, explains, compares, or interprets information using reasoning or evidence.
>
>**Example 1:** CoreWeave buys 8% of NVIDIA chips, NVIDIA backs CoreWeave; what about NVIDIA's revenue?
>
>**Example 2:** Why is the stock market climbing ever since Walsh increased rates?
>

### `hot_take`

>**Definition:** A post that expresses a strong, debatable, or provocative opinion that challenges conventional views.
>
>**Example 1:** How are cryptocurrencies not the dumbest thing ever?
>
>**Example 2:** The AI selloff isn’t about demand, it’s about the cost of money and if the biggest spenders can afford to build.
>

### `reaction`

>**Definition:** A post that expresses an immediate emotional response, such as surprise, excitement, frustration, or disappointment
>
>**Example 1:** I know I'm behind for my age.
>
>**Example 2:** The "sell employee stock purchase plan" immediately strategy. This doesn't seem logical to me based on percentages

### `question` 

>**Definition:** A post that asks for information, clarification, or an explanation without primarily expressing a strong opinion.
>
>**Example 1:** How close to your planned retirement do you make your target date funds
>
>**Example 2:** Since Coreweave has a majoy deal with Anthropic which secured the best junk rating, will this help Coreweave recover?
>
### `personal_experience`

>**Definition:** A post that shares an individual's own experiences, decisions, observations, or lessons learned.
>
>**Example 1:** Limiting my 401k contribution to employer matched level only
>
>**Example 2:** I've been a homeowner for 5 years. These are the biggest things I wish somebody told me on day one
>


### The hardest boundary

**Which two labels:** analysis and hot_take.

**The decision rule I used every time:** If the title mainly explains, compares, or interprets something, it's Analysis, even if the tone is strong or controversial. If it mainly expresses a strong, debatable opinion, it's a Hot Take, even when it includes facts or evidence.


---

## The Dataset

**Where the posts came from:** I collected the posts from `r/investing` subreddit

**How I labelled them:** I have labeled the first 20 posts all by myself(cold) and for the rest I have used GitHub copilot to label them and gone through each one to make sure they are correct.


**Counts per label:**

| Label | Count | Share |
|---|---|---|
|analysis| 59 | 29.3% |
|hot_take| 41 | 20.3% |
|question| 40 | 20% |
|reaction| 37 | 18.4%|
|personal_experience| 22 | 12% |
| **Total** | 201  | 100% |


**Three hard cases**
**1.**
> *The post:* Why is the stock market climbing ever since Walsh increased rates?
>
> *Could have been:* Question or Analysis
>
> *I chose, because:* I chose Analysis because the post is asking about a relationship between two market events: the stock market going up and interest rates increasing. Even though it is written as a question, it is mainly trying to understand and interpret what caused the market to climb.


**2.**
> *The post:*  France is starting to look like a peripheral and that should concern everyone holding euro assets.
>
> *Could have been:* Hot Take or Analysis
>
> *I chose, because:* I chose Hot Take because the post makes a strong and debatable opinion about France and warns people holding euro assets. It does not give enough evidence or explanation to be Analysis, so the main thing it is doing is expressing a strong viewpoint.

**3.**
> *The post:* The "sell employee stock purchase plan" immediately strategy. This doesn't seem logical to me based on percentages
>
> *Could have been:* Reaction or Personal Experience
>
> *I chose, because:* I chose Reaction because the post mainly expresses confusion and disagreement with the strategy. The person does not really explain their own experience with an employee stock purchase plan, so I did not use Personal Experience.

---

## The Training Run

**Device:** device: cpu  (CPU)

**Torch Version:** torch:  2.14.1+cpu

**Base model:** distilbert-base-uncased

**Settings:**
EPOCHS = 3, LEARNING_RATE = 2e-5, BATCH_SIZE = 16, SEED = 42
**Anything I changed from the defaults, and why:** I did not change any default values

**Split sizes:** 
train 139  ·  val 31  ·  test 31
| label | train |  val | test|
|---|---|---|---|                                
|analysis  |            41 |   8 |   11 |
|hot_take  |             29 |   6 |    7 |
|reaction  |              26  | 7 |    4|
|personal_experience |     16 |   2 |     4 |
|question |               27   | 8 |    5|

 `hot_take` has only 7 examples in the test split.

 `reaction` has only 4 examples in the test split.

 `personal_experience` has only 4 examples in the test split.

 `question` has only 5 examples in the test split.


---

## How I Used AI

**Moment 1** 

- *What I asked for:* I have asked the copilot to label the posts based on my taxonomy rules that I have gathered from r/investing subreddit
- *What came back:* It labeled the data, but many of them are incorrectly labeled
- *What I changed:* I went through each one one by one and chnaged the incorrectly labeled labels.

**Moment 2**

- *What I asked for:* In the beginning of the project I asked chatgpt to find me some subreddits with wide variety of posts that can classify as analysis, hot_take and reactions
- *What came back:* It gave so many subreddits, but almost 95% of them are just having questions in them not useful for the classification
- *What I changed:* I have manually checked multiple popular subreddits and checked each of them and finally found r/investing subreddit.

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained
| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy | 0.226 | 0.355 | +0.129 |
| Macro F1 | 0.253 | 0.107 | -0.145 |
| F1 — `analysis` | 0.000 | 0.537 | +0.537 |
| F1 — `hot_take` | 0.133 | 0.000 | -0.133 |
| F1 — `personal_experience` | 0.857 | 0.000 | -0.857 |
| F1 — `question` | 0.000 | 0.000 | +0.000 |
| F1 — `reaction` | 0.273 | 0.000 | -0.273 |


**What I predicted before I looked:**
I expected my trained model to perform best on `analysis` because it appears to have learned that label while failing to recognize the others.

**What the gap actually means:**
My trained model performed worse than the baseline because it became biased toward the `analysis` label and classified nearly every post as analysis. I need to retrain it with clearer, more balanced examples so it can better distinguish between all five categories.



---

## Run Log — Before

**Spread Table:**

| Measure | Seed 42 | Seed 7 | Seed 2024 | Spread |
|---|---|---|---|---|
| Overall accuracy | 0.355 | 0.226 | 0.452 | 0.226 |
| Macro F1 | 0.107 | 0.074 | 0.338 | 0.264 |
| F1 — `analysis` | 0.537 | 0.368 | 0.519 | 0.168 |
| F1 — `hot_take` | 0.000 | 0.000 | 0.000 | 0.000 |
| F1 — `reaction` | 0.000 | 0.000 | 0.600 | 0.600 |
| F1 — `personal_experience` | 0.000 | 0.000 | 0.000 | 0.000 |
| F1 — `question` | 0.000 | 0.000 | 0.571 | 0.571 |

**device: cpu  (CPU)**

**torch:  2.14.1+cpu**

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Every label must have an F1 score of at least 0.50 on the held-out test set for all three seeds. | 5 of 5  |0.5,0.0,0.0,0.0,0.0| 0.36,0.0,0.0,0.0,0.0 | 0.5,0.0,0.6,0.0,0.57 | MISS |
| 2. The hot_take label can perform worse than the other labels, but it should still have an F1 score of at least 0.40 on the held-out test set across all three seeds. |  3 of 3 | 0.0 | 0.0 | 0.0  | MISS |
| 3. The model must correctly identify at least one true hot_take post in the held-out test set for each of the three seeds.  | 3 of 3 | 0 | 0 | 0 | MISS |
| 4. When two people label the same 30 posts using the same definitions, they should agree on at least 80% of the time.  | 24 of 30| MET | MET | MET | MET |
| 5. For each seed, the model should be more accurate on its most-confident third of predictions than on its least-confident third of predictions.  | 3 of 3 | 0.8>0.0 | 0.4>0.1 | 0.7>0.4 | MET |



### Confusion matrix

| true \ predicted | analysis | hot_take | reaction | personal_experience | question |
|---|---|---|---|---|---|
| **analysis** | 11 | 0 | 0 | 0 | 0 |
| **hot_take** | 7 | 0 | 0 | 0 | 0 |
| **reaction** | 4 | 0 | 0 | 0 | 0 |
| **personal_experience** | 3 | 1 | 0 | 0 | 0 |
| **question** | 5 | 0 | 0 | 0 | 0 |


**My biggest off-diagonal number, and what it means:**
Looking at the confusion matrix, I can see that the model predicted
`analysis` for 30 of the 31 posts. It correctly identified all 11 actual
`analysis` posts, but it also labeled 7 `hot_take`, 4 `reaction`, 3
`personal_experience`, and 5 `question` posts as `analysis`. The only other
prediction was a `personal_experience` post labeled as `hot_take`. The model
did not predict any posts as `reaction`, `personal_experience`, or `question`.
This shows that the model has become heavily biased toward `analysis` instead
of learning the differences between the categories. I need to review and
rebalance the training examples, especially the boundaries between `analysis`
and the other labels, so each category has clearer and more consistent
examples.

---

## Verdicts and Diagnoses
| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Every label must have an F1 score of at least 0.50 on the held-out test set for all three seeds. | 5 of 5 | MISS | Not even one label has F1 score of atleast 0.50 across all three seeds |
| 2 | The hot_take label can perform worse than the other labels, but it should still have an F1 score of at least 0.40 on the held-out test set across all three seeds. | 3 of 3 | MISS | hot_take label has 0.0 recall across all three seeds  |
| 3 | The model must correctly identify at least one true hot_take post in the held-out test set for each of the three seeds. | 3 of 3 | MISS | It did not identify even one post as hot_take because in every seeds confusion matrix, it didn't even classify one hot_take post correctly as hot take |
| 4 | When two people label the same 30 posts using the same definitions, they should agree on at least 80% of the time.   | 24 of 30  | MET | I asked 2 of my friends to label the same posts, and we agreed on 26 out of 30. That is above 80%, so it is met |
| 5 | For each seed, the model should be more accurate on its most-confident third of predictions than on its least-confident third of predictions. | 3 of 3 | MET | For every seed, the model's most confident third of predictions have high score than the least confident theird of predictions. |

**Diagnoses**
**Criterion 1:** The model labeled almost every post as `analysis`, and it did not learn how to tell the five categories apart. The confusion matrix also shows that 30 out of 31 posts were classified as `analysis`, so I think I need to train the model more.

**Criterion 2:** The model had an F1 score of 0 for `hot_take` in all three seeds. Based on my agreement report, I also sometimes confused `hot_take` with `analysis`, so I think I need to provide clearer examples showing the difference between these two labels.

**Criterion 3:** The model did not correctly identify even one `hot_take` post in any of the three runs. I think this probably happened because there were not enough clear and balanced `hot_take` examples for the model to learn from.


---

## Agreement Report


**Agreement rate:** 24 / 30 = 86.7%


**Disagreements**

**1.**
> *The post:* "The club championship scoring changed in 2019 from top-6 to top-10. Since then our B team has finished above the A team twice. That's not depth improving, it's the scoring rewarding turnout."
>
> *Staff said / I said:* analysis
>
> *My call, and why:* hot_take, because eventhough they showed why they have won, I felt that writer already reached a conclusion and the numbers are just for support,but when reading again I think analysis suits better because they are trying to state the fact why their team had improved
>
> *Which pile:* the rule covered it and I applied it loosely


**2.**
> *The post:* "Carbon plates aren't the whole story. My times dropped 2% in the shoes and another 2% the following year in the same pair, when the only thing that changed was going from 35 to 50 miles a week."
>
> *Staff said / I said:* analysis
>
> *My call, and why:* hot_take, I initially marked it as analysis, but when I read that again, I felt that author is claiming that she ran more miles eventhough her dropping of rate is same as last year but thisn't due to carbon plating. I didn't see analysis there
>
> *Which pile:*  the rule covered it and I applied it loosely

**3.**
> *The post:* Got up at 5, drove ninety minutes, and it's cancelled. Standing in the car park in the rain reading the email."
>
> *Staff said / I said:* reaction
>
> *My call, and why:* analysis, there is no reaction there, he's just standing in the parking lot reading he cancellation email and didn't express anything. There isn't any response from his side so I didn't know which to mark, and it isn't a hot_take so I marked it as analysis.
> *Which pile:* the rule is ambiguous here and my reading is defensible

**4.**
> *The post:* "Wind was so bad on the out section I was leaning at about 20 degrees. Coming back felt like cheating.",
>
> *Staff said / I said:* reaction
>
> *My call, and why:* hot_take, I thought this was a hot_take because they are claiming that wind outside is very bad and used number just to support that, but reading it again I agree with that being a reaction
>
> *Which pile:*  the rule covered it and I applied it loosely

**What the pattern in my disagreements tells me:**
Patterns in my disagreements tells me that I sometimes focused too much on strong wording or specific details instead of identifying the main purpose of each post. I treated posts with numbers as analysis and posts with strong statements as hot takes, even when they were mainly expressing an immediate reaction or experience. This helped me realize that I need to ask whether the post is primarily explaining evidence, expressing a debatable opinion, or sharing an immediate response.


---

## The Improvement

**What I changed:** I have changed the learning rate to 3e-5 from 2e-5  and also increased the no.of epochs from 3 to 6

**Which diagnosis pointed at it:** At first, my model predicted almost every post in the test set as `analysis`, so I felt that it was becoming biased toward that category and was not learning how to tell the labels apart. To improve this, I experimented with the learning rate and increased the number of epochs to see if more consistent updates and extra training would help the model recognize the other categories.

### Run Log — After


| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Every label must have an F1 score of at least 0.50 on the held-out test set for all three seeds. | 5 of 5  |0.81,0.28,0.0,0.0,0.67| 0.41,0.36,0.0,0.0,0.71 | 0.51,0.22,0.6,0.0,0.67 | MISS |
| 2. The hot_take label can perform worse than the other labels, but it should still have an F1 score of at least 0.40 on the held-out test set across all three seeds. |  3 of 3 | 0.28 | 0.36 | 0.22  | MISS |
| 3. The model must correctly identify at least one true hot_take post in the held-out test set for each of the three seeds.  | 3 of 3 | 2/5 | 2/5 | 1/5 | MET |
| 4. When two people label the same 30 posts using the same definitions, they should agree on at least 80% of the time.  | 24 of 30| MET | MET | MET | MET |
| 5. For each seed, the model should be more accurate on its most-confident third of predictions than on its least-confident third of predictions.  | 3 of 3 | 0.8>0.2 | 0.6>0.1 | 0.7>0.4 | MET |


**Did it help, and how do I know:**

     Criterion 3 was met after improving the model so that it correctly identified at least one `hot_take` post in the test set. While this may seem like a small improvement, I consider it significant because the model started recognizing multiple labels instead of classifying every post as `analysis`. This progress can also be seen in the changes to the accuracy, F1 score, and per-label macro scores before and after the improvements.



---

## What's Still Broken

Criteria 1 and 2 are still not met. The model did not achieve an F1 score of at least 0.50 for every label, and the hot_take F1 score stayed below 0.40 for all three seeds. I would improve this by relabeling the data using the correct label boundaries and adding more examples to the weaker classes so that the classes are more balanced and the model can learn more effectively. I stopped here because I ran out of time, but I plan to continue training and improving my model in my free time so that it can classify multiple labels more accurately instead of relying mostly on the analysis label.



**The gap between what I meant my labels to capture and what the model
learned:**

     I intended `reaction` to describe an immediate response and `personal_experience` to describe someone sharing their own experience, but the model often confused both labels with `analysis` or `hot_take`. The confusion matrices show this clearly where `reaction` was frequently predicted as `analysis`, while `personal_experience` was never correctly identified for any of the three seeds, which suggests that the model has not learned reliable boundaries between these categories.



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
