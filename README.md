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
|analysis  |            40 |   8 |   11 |
|hot_take  |             28 |   6 |    7 |
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

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



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
