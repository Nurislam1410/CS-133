# Will AI Replace Us?

**Mapping how data scientists talk about AI driven job displacement on LinkedIn**

CS 133 Data Visualization, San José State University, Fall 2026
Team: Dan Nguyen, Nurislam Saliev, Rohan Poosala

## About the project

Layoffs are increasingly blamed on AI, and job insecurity is a known source of stress. Data scientists and AI practitioners build and understand these tools better than most people, so how they talk about AI taking their jobs says a lot. As students about to enter the same job market, this question is personal for us too.

We explore whether data science practitioners sound more anxious or more confident about AI, and whether that depends on which AI capability they are discussing (LLM agents, AutoML, vibe coding and more).

**Prediction question:** Can a post's topic profile plus its length predict its sentiment category (Optimistic, Balanced or Anxious)?

## Dataset

| | |
|---|---|
| Source | CORA / Dataverse CSUC, Universitat Pompeu Fabra |
| DOI | [10.34810/DATA3307](https://doi.org/10.34810/DATA3307) |
| License | CC0 (open access) |
| Size | 784 LinkedIn posts, April 2024 to June 2025 |
| Columns | Raw post text, preprocessed text, probabilities for 7 LDA topics |

Our names for the 7 topics, based on their top words:

| Topic | Name | Posts |
|---|---|---|
| Topic1 | Will AI replace us? | 642 |
| Topic5 | LLM agents at work | 67 |
| Topic2 | AutoML automating ML | 23 |
| Topic4 | ChatGPT doing analysis | 17 |
| Topic3 | Vibe coding with GenAI | 13 |
| Topic6 | Juniors and citizen devs | 11 |
| Topic7 | Engineering skills for AI era | 11 |

**Loading the CSV:** the file uses semicolons between columns and commas as decimal points, and has 215 blank rows at the end.

```python
df = pd.read_csv(DATA_PATH, sep=';', decimal=',')
df = df.dropna(how='all')   # 784 rows
```

The CSV is not stored in this repo. Download it from the DOI link above and set `DATA_PATH` in the notebook.

## Repository contents

```
CS-133/
├── Notebooks/
│   ├── P1_initial_exploration.ipynb   # data types, missing data, relplot, catplot, small multiples
│   └── P2_EDA_questions.ipynb         # filtering, scatter, distribution, interactive Plotly line
├── CS 133 Project Proposal.pptx.pdf   # proposal slides
├── Part 1_ Project Proposal .pdf      # proposal write up
└── README.md
```

## Key findings so far

The file has no sentiment labels, so we gave each post a first pass tone label by counting anxiety words (fear, layoff, obsolete) against optimism words (opportunity, upskill, augment).

1. **Topics:** 82% of posts are the broad "Will AI replace us?" debate; five topics have fewer than 25 posts.
2. **Tone:** 55% of posts lean optimistic, 26% are balanced and 19% lean anxious, matching the paper's conclusion.
3. **Worry by topic:** posts about ChatGPT for analysis (35% anxious) and vibe coding (31%) are the most worried; AutoML is the calmest (9%). These groups are small.
4. **Mixed posts:** anxiety and optimism word counts are almost unrelated, so many posts name a fear and then answer it.
5. **Post length:** short posts use the most emotional language; optimism stays above anxiety at every length.

## Approach

* **Tools:** Python, Google Colab, pandas, seaborn, Plotly, scikit-learn
* **Algorithms:** LDA topic scores (provided), lexicon based tone label, logistic regression; possible upgrade to a zero shot or transformer sentiment model
* **Testing:** 80/20 train and test split, k fold cross validation on the training set, accuracy and F1 against a majority class baseline, rechecks without outlier length posts, manual spot checks of labels

## Team workflow

Work on a branch and open a pull request instead of pushing to `main`:

```bash
git checkout -b my-feature
git add <files>
git commit -m "Describe the change"
git push -u origin my-feature
gh pr create --reviewer <teammate>
```

## References

* Samokhina, O. (2026). Technological optimism or automation anxiety: how data scientists discuss AI driven job displacement. *Hipertext.net*, 32.
* Dataset: CORA / Dataverse CSUC, DOI 10.34810/DATA3307. Based on a Master's dissertation (DiCEM, Universitat Pompeu Fabra, 2024 to 2025).
* Blei, D., Ng, A., & Jordan, M. (2003). Latent Dirichlet Allocation. *Journal of Machine Learning Research*.

