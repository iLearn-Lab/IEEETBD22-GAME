# Multi-Relation Extraction via A Global-Local Graph Convolutional Network

> GAME — a global-local graph convolutional network for multi-relation extraction that jointly models sentence-level global structure and entity-level local context.

## Authors

**Harry Cheng**<sup>1</sup>, **Lizi Liao**<sup>2</sup>, **Linmei Hu**<sup>3</sup>, **Liqiang Nie**<sup>1</sup>\* 

<sup>1</sup> Shandong University
<sup>2</sup> Singapore Management University,
<sup>3</sup> Beijing University of Posts and Telecommunication
\* Corresponding author

## Links

- **Paper**: [IEEE Xplore](https://ieeexplore.ieee.org/document/9684942/)
- **Dataset (NYT train)**: [Google Drive](https://drive.google.com/file/d/1ukDBUeTjAAwO4ccnSONe9tTRemGcLk0L/view?usp=share_link)
- **Dataset (NYT test)**: [Google Drive](https://drive.google.com/file/d/1OEHnEuR0vvO-F_JSfjoaEJ2OZYezKaMC/view?usp=share_link)

---

## Table of Contents

- [Updates](#updates)
- [Introduction](#introduction)
- [Highlights](#highlights)
- [Method / Framework](#method--framework)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Dataset / Benchmark](#dataset--benchmark)
- [Usage](#usage)
- [TODO](#todo)
- [Citation](#citation)
- [Acknowledgement](#acknowledgement)
- [License](#license)

---

## Updates

- [04/2026] Transfer repos to iLearn-Lab
- [2022] Paper published in IEEE Transactions on Big Data, Vol. 8, No. 6, pp. 1716–1728

---

## Introduction

This repository is the official implementation of **Multi-Relation Extraction via A Global-Local Graph Convolutional Network**, published in **IEEE Transactions on Big Data**.

Relation extraction identifies semantic relations between entity pairs in text. Many sentences contain multiple overlapping entity pairs and relations simultaneously — a challenge that sequential models handle poorly.

**GAME** (Global-local grAph convolutional network for Multi-relation Extraction) addresses this with two GCN layers of different structures:
- A **global** layer capturing sentence-level syntactic dependencies
- A **local** layer capturing entity-centric relational context

These complementary representations are combined for joint multi-relation classification.

---

## Highlights

- Jointly models **global** (sentence-level) and **local** (entity-level) graph structure
- Handles **overlapping triplets** within the same sentence
- Evaluated on **NYT** (public) and **TACRED** benchmarks
- GCN layers implemented via both pure GCN and graph attention network (GAT) for ablation

---

## Method / Framework

GAME constructs a dependency-based graph over sentence tokens and augments it with entity-centric local edges. Two GCN layers with different structures encode complementary global and local representations. The resulting entity embeddings are fed into a relation classifier for multi-relation prediction.

---

## Project Structure

```text
.
├── GCN_RE/                # Core GCN-based relation extraction module
│   └── utils/             # Preprocessing and data utilities
├── Spacy_preprocess.py    # Spacy-based syntactic preprocessing
├── eval.py                # Evaluation script
├── test_dataset.py        # Dataset testing utility
├── train.py               # Training script
└── README.md
```

Data should be placed in:

```text
data/
└── nyt/
    ├── train.json
    └── test.json
```

---

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/iLearn-Lab/IEEETBD22-GAME.git
cd IEEETBD22-GAME
```

### 2. Create environment

```bash
python -m venv .venv
source .venv/bin/activate   # Linux / Mac
# .venv\Scripts\activate    # Windows
```

### 3. Install dependencies

```bash
pip install -U pip setuptools wheel
pip install -U spacy
python -m spacy download en_core_web_md
```

For GPU-accelerated Spacy, see the [official installation guide](https://spacy.io/usage).

---

## Dataset / Benchmark

- **NYT train.json**: [Google Drive](https://drive.google.com/file/d/1ukDBUeTjAAwO4ccnSONe9tTRemGcLk0L/view?usp=share_link)
- **NYT test.json**: [Google Drive](https://drive.google.com/file/d/1OEHnEuR0vvO-F_JSfjoaEJ2OZYezKaMC/view?usp=share_link)

Place data files in `./data/nyt/` and update paths in `train.py` and `eval.py`.

**TACRED** requires a paid license from [LDC](https://catalog.ldc.upenn.edu/LDC2018T24) and is not redistributed here.

### Data Format

```json
{
  "sentence": ["token1", "token2", "..."],
  "subj_start": 27,
  "subj_end": 28,
  "obj_start": 10,
  "obj_end": 11,
  "relation": "/people/person/children",
  "edges": [[2, 0], [2, 1], "..."]
}
```

Sentences with multiple relations appear multiple times (one entry per relation). To customize preprocessing, modify files in `GCN_RE/utils/`.

---

## Usage

### Training

```bash
python train.py
```

### Evaluation

```bash
python eval.py
```

Update data and model paths in the respective scripts before running.

---

## Citation

If you find our work useful, please cite:

```bibtex
@article{cheng2022game,
  title   = {Multi-Relation Extraction via A Global-Local Graph Convolutional Network},
  journal = {IEEE Transactions on Big Data},
  volume  = {8},
  number  = {6},
  pages   = {1716--1728},
  year    = {2022},
}
```

---

## Acknowledgement

- Thanks to the creators of the NYT and TACRED datasets.
- Thanks to the [Spacy](https://spacy.io/) team for their excellent NLP library.

---

## License

This project is released under the Apache License 2.0.
