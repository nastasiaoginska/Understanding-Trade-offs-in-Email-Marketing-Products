# Understanding Trade-offs in Email Marketing Products  
**Data-driven market landscape analysis using unsupervised data mining**
## Overview

This project explores the **email marketing software market** through the lens of **perceived value (pros)** and **perceived pain points (cons)**.  
Using unsupervised data mining techniques, it aims to uncover:

- how the market is structurally organized,
- which **product archetypes** naturally emerge,
- what **trade-offs** are systematically embedded in the market,
- and where **white space** may exist for new product directions.

The result is a **market map**, a **competitive landscape**, and a set of **interpretable trade-off patterns** derived directly from customer-facing perceptions.

## Business Question

> **How is the email marketing market structured by value propositions, pains, and trade-offs — and where is there room for a new product archetype?**

This project intentionally avoids prediction. Its goal is **structure discovery**, not forecasting.

## Data

**Unit of analysis:** one product (one row per product).

**Fields used in the analysis:**
- `name`
- `pros_themes` — predefined positive themes selected by users (semicolon-separated)
- `cons_themes` — predefined negative themes selected by users (semicolon-separated)

Additional metadata (ratings, number of reviews, pricing, market segment) is available but not required for the core unsupervised analysis.

### Notes on data semantics

- Pros and cons are chosen from a **predefined set of themes** on the source platform.
- This ensures **consistent labeling across products**, which makes cross-product comparison reliable.
- Themes represent **high-level signals**, not detailed explanations.  
  For example, *“Missing Features”* indicates perceived lack of functionality but does not specify which exact features are missing.

## Methodology (CRISP-DM aligned)

### 1. Data Preparation

- Parse `pros_themes` and `cons_themes` into long format.
- Build a **binary product × theme matrix** (presence / absence).
- Prefix themes with `PRO__` and `CON__` to preserve polarity.
- Prune rare themes to reduce noise and improve interpretability.

**Artifact:**  
`feature_matrix_pruned` — products × themes (binary)

### 2. Similarity & Clustering (Market Archetypes)

- Compute product similarity using **cosine similarity** over shared themes.
- Apply **hierarchical clustering** to discover natural groupings.
- Describe each cluster by its most frequent PRO and CON themes.

This produces:
- natural **product archetypes**,
- a **competitive map**,
- interpretable cluster profiles.

### 3. Co-occurrence Analysis (Trade-offs)

Co-occurrence answers questions like:
- *Which pains tend to come together?*
- *Which values systematically coexist with certain limitations?*

We analyze:
- **CON–CON** co-occurrence (pain bundles),
- **PRO–CON** co-occurrence (value–trade-off relationships),

using:
- co-occurrence counts,
- conditional probabilities,
- **lift** (unexpectedness vs baseline frequency).

High lift + meaningful support indicates **structural market patterns**, not coincidences.

## Key Findings

### Market core (dominant perceptions)

**Most common PRO themes:**
- Ease of Use
- Customer Support
- Helpful / Intuitive / Simple

**Most common CON themes:**
- Missing Features
- Limited Features
- Learning Curve
- Expensive (segment-dependent)
- Limited Customization

### Structural market tension

**Missing / Limited Features is a systemic pain**, not an isolated defect.

It frequently co-occurs with:
- Ease of Use
- Easy Creation
- Intuitive / Simple experiences

This reveals a recurring market trade-off:

> **Ease of use is often achieved at the cost of depth and control.**

### CON–CON “pain bundles”

Negative perceptions tend to cluster together:

- Missing Features ↔ Limited Features  
- Missing Features ↔ Learning Curve  
- Limited Features ↔ Limited Customization / Template Limitations  

Products rarely suffer from just one constraint — they inherit **packages of limitations**.

### White space hypothesis

The results indicate potential whitespace around value combinations that are rarely delivered together in the current market.

While individual dimensions such as ease of use, design focus, or fast creation are well represented, their combination with deeper control and predictable output appears structurally constrained by existing trade-offs.
