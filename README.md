

It's 1999. Inboxes are filling up with junk, and you're the new programmer told to stop it. Back then, spam filters weren't clever at all: just hand-written keyword lists ("block anything that says *Free"), blocklists of known spammers, and rules for blocking suspicious servers.

This notebook puts you in those shoes. You'll build a 1999-style spam filter by hand on 5,572 real text messages: a keyword list, then a blocklist, then more and more rules. You'll watch them misfire, discover that clues need weights, tune those weights yourself, and get ambushed by spammers who change their spelling. Then the story jumps to 2002, when Paul Graham's essay *"A Plan for Spam"* made Bayesian filtering famous. You'll do what he did, and a four-line machine learning model beats your best effort and even teaches you something about the data.

Every code cell is commented line by line, so you only need basic Python to follow along.

By the end, one idea should feel obvious rather than memorised:

> **Traditional programming:** you write the rules, the computer gives you answers.
> **Machine learning:** you give the computer examples and answers, and it writes the rules.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR-USERNAME/YOUR-REPO/blob/main/notebooks/01_rules_vs_learning.ipynb)

## 📖 Reading along with Géron

The story follows the spam filter example that opens Chapter 1 ("The Machine Learning Landscape") of Aurélien Géron's *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow* (O'Reilly). Géron uses spam to explain why machine learning exists. This notebook lets you live through it with real data, and 📖 notes along the way point back to the relevant parts of the chapter. Any edition works, including the earlier *...with Scikit-Learn and TensorFlow*.

## What's in the repo

```
.
├── notebooks/
│   └── 01_rules_vs_learning.ipynb             # start here: the story, with "Your turn" gaps to fill
├── solutions/
│   └── 01_rules_vs_learning_solutions.ipynb   # the same story with every gap filled and spoilers revealed
├── data/
│   └── README.md                              # where the dataset comes from
├── requirements.txt
└── README.md
```

Work through the notebook in `notebooks/` first. Peek at `solutions/` only when you're stuck or finished.

## How the story unfolds

- **Prologue: 1999.** How spam filters worked before machine learning, plus a short timeline of the spam war.
1. **The job.** What a spam filter has to do, the two ways to build one, and why the old way was so hard.
2. **Before you touch the keyboard.** A few questions to get you thinking like a filter.
3. **Meet the data.** Load real messages, fix a messy CSV, and split off a test set you're not allowed to look at.
4. **Keeping score.** Accuracy, precision, recall and F1, and why a filter that catches nothing can still be 86.6% "accurate".
5. **Attempt #1: the keyword list.** One rule. It goes about as well as you'd expect.
6. **Attempt #2: the blocklist.** Block every spammer's phone number you've seen. It looks perfect...
7. **Attempt #3: more keywords.** Lots of rules. It gets messy.
8. **Attempt #4: let the clues vote.** Clues get weights, and you realise you've built a machine learning model by hand.
9. **The moment of truth.** Your filters meet the test set, the blocklist falls apart, and you meet overfitting.
10. **The spammers strike back.** `FR33 pr!ze`.
11. **Stepping back.** Does adding more rules actually help?
12. **2002: enter machine learning.** Paul Graham's Bayesian idea, in four lines of scikit-learn. It beats your best effort and shows you which words it found most spammy.

Here's how the filters end up doing on the test set:

| Filter | Precision | Recall | F1 |
|---|---|---|---|
| Label everything as ham | 0.000 | 0.000 | 0.000 |
| One keyword ("free") | 0.815 | 0.295 | 0.433 |
| Blocklist of spammers' phone numbers | 1.000 | 0.523 | 0.687 |
| A chain of `if` / `elif` rules | 0.765 | 0.503 | 0.607 |
| Hand-tuned weighted score | 0.992 | 0.839 | 0.909 |
| Naive Bayes (learned in under a second) | 0.965 | 0.913 | 0.938 |

## Getting started

**Easiest: Google Colab.** Click the badge above. Nothing to install, and the notebook downloads the data for you.

**Or run it on your own machine:**

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPO.git
cd YOUR-REPO
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/01_rules_vs_learning.ipynb
```

The first time you run it, the notebook downloads `spam.csv` and saves a copy in `data/`.

## The dataset

The [SMS Spam Collection](https://archive.ics.uci.edu/dataset/228/sms+spam+collection), in its Kaggle `spam.csv` form: 5,572 English text messages, 4,825 normal and 747 spam. Details and citation are in [`data/README.md`](data/README.md).

## Teaching with it?

The notebook works for a 90-minute class session. A few tips:

- **Let people struggle a little.** Case sensitivity, `"won"` matching *won't*, and `"call"` turning up in ordinary messages are deliberate stumbling blocks.
- **Keep the test set locked away** until Section 9, so overfitting is something learners discover, not something they're told about.
- **Section 8 is the turning point.** Once learners realise their weighted rule is a linear classifier, the next lesson (how a model learns its weights) follows naturally.
- **Good discussion question:** "Are hand-written rules ever the right answer?" (Think: tiny datasets, legal duties to explain decisions, launching before you have any labels. Real systems like bank fraud detection and SpamAssassin mix rules with learned weights.)

## Further reading

- Géron, A. *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow.* O'Reilly. Chapter 1. Companion code: [ageron/handson-ml3](https://github.com/ageron/handson-ml3)
- Samuel, A. L. (1959). *Some Studies in Machine Learning Using the Game of Checkers.* IBM Journal of Research and Development.
- Mitchell, T. M. (1997). *Machine Learning*, Chapter 1. McGraw-Hill.
- Domingos, P. (2012). *A Few Useful Things to Know About Machine Learning.* Communications of the ACM, 55(10).
- Graham, P. (2002). [*A Plan for Spam.*](http://www.paulgraham.com/spam.html)
- Sahami, M., Dumais, S., Heckerman, D., & Horvitz, E. (1998). *A Bayesian Approach to Filtering Junk E-Mail.* AAAI Workshop on Learning for Text Categorization.
- Almeida, T. A., Gómez Hidalgo, J. M., & Yamakami, A. (2011). *Contributions to the Study of SMS Spam Filtering: New Collection and Results.* ACM DocEng 2011.
- [scikit-learn: Working With Text Data](https://scikit-learn.org/stable/tutorial/text_analytics/working_with_text_data.html)

## Author

Uthkarshi Perera
