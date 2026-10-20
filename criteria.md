# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.


---

## 1. Every label must have an F1 score of at least 0.50 on the held-out test set for all three seeds.

**Why this target:**
I want the model to recognize all five categories instead of doing well only on the most common ones. An F1 score of 0.50 seems like a reasonable minimum because it shows the model is doing better than simply guessing, while still allowing for the fact that some labels have fewer examples.

---

## 2.The hot_take label can perform worse than the other labels, but it should still have an F1 score of at least 0.40 on the held-out test set across all three seeds.

**Why this target:**
My dataset has fewer hot_take examples, so the model has less information to learn from and its score may vary more between seeds. I am allowing it to have a lower score, but I still want the model to recognize hot_take posts often enough for the category to be useful.

---

## 3. The model must correctly identify at least one true hot_take post in the held-out test set for each of the three seeds.

**Why this target:**
Since hot_take is the minority class, I do not want the model to ignore it and classify those posts as one of the other labels. This target makes sure the model is recognizing at least some hot_take posts instead of avoiding the category completely.

---

## 4.When two people label the same 30 posts using the same definitions, they should agree on at least 80% of the time.

**Why this target:**
Some posts may be difficult to place because they fall between two categories, so I do not expect perfect agreement. However, an 80% agreement rate would show that the labeling rules are clear enough for two people to use them consistently.

---

## 5.For each seed, the model should be more accurate on its most-confident third of predictions than on its least-confident third of predictions.

**Why this target:**
Clearer posts should result in more confident predictions, while posts that are harder to classify should produce less confident predictions. This criterion checks whether the model’s confidence scores actually give a useful indication of how likely its predictions are to be correct.


---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
