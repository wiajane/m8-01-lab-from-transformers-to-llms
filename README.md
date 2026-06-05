![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Lab | Inside the Tokenizer

## Overview

Before an LLM sees a single word, a tokenizer chops your text into tokens. Today you'll get hands-on with that hidden first step — the one that explains API costs, context limits, and half the "why did the model do *that*?" moments you'll hit all week.

No API keys, no GPU. You'll tokenize real text with a couple of different tokenizers, hunt down the weird cases, and build a small token-and-cost estimator. The deliverable is one notebook with your code, outputs, and short written observations.

This lab reinforces the in-lesson exercise from today's lecture — treat it as the longer, graded version.

## Learning Goals

By the end of this lab you should be able to:

- Tokenize text with real tokenizers and read the resulting tokens and IDs
- Explain why token counts differ across text types (English, code, other languages, emoji)
- Estimate the token count and API cost of a piece of text before you ever send it

## Setup

Fork this repo, clone it, and work on a branch. You'll need Python 3.10+ and a couple of libraries:

```bash
pip install tiktoken transformers
```

- [`tiktoken`](https://github.com/openai/tiktoken) gives you a fast BPE tokenizer.
- [`transformers`](https://huggingface.co/docs/transformers) lets you load other tokenizers (e.g. a Llama or Gemma tokenizer) from the Hugging Face Hub. A second tokenizer is enough — you do **not** need to download any model weights, only the tokenizer.

Work in `tokenizer_explorer.ipynb`. If you can't install `transformers`, a single tokenizer via `tiktoken` is acceptable for Tasks 1 and 3; note the limitation in your notebook.

## Tasks

You have **three** tasks. Keep code readable and put your written observations in Markdown cells.

### Task 1 — Tokenize and compare

Pick a paragraph of mixed content — a couple of English sentences, a line of code, a few words in another language, and an emoji or two. Then:

1. Tokenize it with **at least two** different tokenizers.
2. For each, print the **tokens** (the actual sub-word strings) and the **token IDs**.
3. Show the **token count** from each tokenizer side by side in a small table.

In a Markdown cell, answer: **where do the two tokenizers disagree most, and why might that be?**

### Task 2 — Hunt the weird cases

Tokenizers behave in surprising ways. Investigate **at least three** of the following and show the token counts that prove your point:

- A long rare/made-up word vs. a common word of similar length
- The same sentence in English vs. another language
- A snippet of code or JSON vs. an equivalent amount of prose
- A word repeated with and without a leading space (e.g. `"hello"` vs `" hello"`)
- An emoji or accented characters

For each case, write one sentence in a Markdown cell explaining **what you observed and why it matters** for cost or the context window.

### Task 3 — Token + cost estimator

Write a small function `estimate(text, price_in, price_out, expected_output_tokens)` that:

1. Counts the input tokens in `text` using one of your tokenizers.
2. Takes a price-per-1K-tokens for input and output, plus an expected number of output tokens.
3. Returns (and prints) the **input token count** and the **projected total cost** (input + output).

Then run it on three different inputs (e.g. a short question, a long document, a code file) using a small made-up price table, and show the results. Add one Markdown sentence: **which input is most expensive, and is it what you expected?**

## Submission

Open a Pull Request to the lab repository containing:

```
tokenizer_explorer.ipynb     # code, outputs, and your Markdown observations
```

Make sure the notebook is **run** (outputs visible) before you commit. Paste the PR link as your deliverable.

## Quality bar

You'll be reviewed on:

- **Do the outputs actually appear** in the committed notebook, or is it code with no results?
- **Are the observations specific** ("Thai cost 3.2× the English tokens") or vague ("it was different")?
- **Does the estimator handle all three inputs** and report both token count and cost?

Three small artifacts in one notebook. Make the observations sharp.
