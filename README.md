# NLP Word Segmentation & POS Tagging

Word segmentation and Part-of-Speech (POS) tagging with classic probabilistic models: **trigram language models + dynamic programming** for segmentation, and a **Hidden Markov Model (HMM) + Viterbi decoding** for tagging. Includes a morphology-aware tagging variant for Spanish, baseline comparisons, confusion-matrix evaluation, and error analysis.

## Problem Statement

1. **Word segmentation:** given text with no word boundaries (e.g. `thecatsat`), recover the most likely word sequence (`the cat sat`).
2. **POS tagging:** given a sentence, assign each word its most likely grammatical tag.
3. **Joint view:** study how segmentation mistakes propagate into tagging errors.

## Approach

### Word Segmentation
- A **trigram language model** scores candidate word sequences: `P(w_i | w_{i-2}, w_{i-1})`.
- **Dynamic programming** searches over all possible split points instead of enumerating every segmentation, so the best segmentation is found efficiently.
- **Baseline:** greedy longest-match segmentation, which makes locally optimal choices and cannot recover from early mistakes.

### POS Tagging
- **HMM tagger:** tags are hidden states, words are observations.
  - Transition probabilities: `P(tag_i | previous tag(s))`
  - Emission probabilities: `P(word | tag)`
- **Viterbi decoding** finds the single most likely tag sequence for a sentence.
- **Baseline:** a simpler non-contextual tagger for comparison.

### Morphology-Aware Tagging (Spanish)
- Spanish is morphologically rich (verb conjugations, gender/number agreement), so many surface forms are rare or unseen.
- Morphological information (such as word endings) is used to help tag words the model has not seen often.

## Results

Accuracy values recorded in the notebook's saved outputs:

| Task | Approach | Accuracy |
|---|---|---:|
| English POS tagging | HMM | 95.12% |
| English POS tagging | Baseline | 93.73% |
| Spanish POS tagging | HMM | 91.55% |
| Spanish POS tagging | Baseline | 88.60% |
| Spanish morphology-aware tagging | HMM | 89.11% |
| Spanish morphology-aware tagging | Baseline | 85.38% |

## Evaluation & Error Analysis

- **Accuracy** for model-vs-baseline comparison.
- **Confusion matrices** to see which tags get confused (e.g. noun vs. verb, adjective vs. noun).
- **Error breakdown:** separating errors caused by incorrect segmentation from errors made by the tagger itself.

## Tech Stack

Python · NLTK · NumPy / pandas · Google Colab

## Repository Structure

```text
nlp-segmentation-pos-tagging/
├── README.md
└── notebooks/
    └── Word_Segmentation_POS.ipynb
```

## How to Run

1. Open `notebooks/Word_Segmentation_POS.ipynb` in Google Colab.
2. Install/import the required libraries.
3. Point the dataset paths to your own data (or mount Google Drive if needed).
4. Run all cells in order to train and evaluate.

## Limitations

- Trigram models only see a two-word context, so long-range dependencies are missed.
- Unseen words and n-grams hurt both segmentation and tagging unless smoothing/morphology handling covers them.
- HMMs assume each tag depends only on the previous tag(s), which is a strong simplification.

## Project Type

Group academic project. My contributions: model implementation and evaluation. 
