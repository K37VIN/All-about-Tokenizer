# 🚀 Byte-Level BPE Tokenizer (From Scratch)

A production-style **Byte Pair Encoding (BPE) Tokenizer** implemented from scratch in Python.

This project demonstrates:

- ✅ Byte-level BPE (GPT-2 style)

- ✅ Parallel pair counting for faster training

- ✅ Modular pre-tokenizer system

- ✅ Deterministic merge ranking

- ✅ Encode / Decode functionality

- ✅ Save / Load support

- ✅ Performance benchmarking

---

## 📚 Table of Contents

- Overview

- Architecture

- Features

- Installation

- Usage

- Benchmarking

- Design Decisions

- Project Structure

- Future Improvements

---

# 🔎 Overview

Byte Pair Encoding (BPE) is a subword tokenization algorithm widely used in modern Large Language Models such as GPT, RoBERTa, and BERT.

This project implements a **byte-level BPE tokenizer**, meaning:

- It operates on UTF-8 bytes instead of characters

- It can tokenize any Unicode input (including emojis)

- It avoids unknown token issues

- It mimics real-world tokenizer behavior

---

# 🏗 Architecture

The project is structured into modular components:

`Tokenizer System
│
├── PreTokenizer (Base Class)
│   ├── SimplePreTokenizer
│   └── BytePreTokenizer
│
├── BPETrainer
│   ├── Parallel Pair Counting
│   └── Iterative Merge Learning
│
├── BPETokenizer
│   ├── encode()
│   ├── decode()
│   ├── save()
│   └── load()
│
└── Benchmark Utility`

---

# ✨ Features

## 🔹 1. Byte-Level Tokenization

Instead of splitting into characters:

`"H" → 72
"i" → 105`

The tokenizer works directly on:

`b'H'
b'i'`

This ensures compatibility with:

- Multilingual text

- Emojis

- Rare Unicode characters

---

## 🔹 2. Parallel Pair Counting

During training, pair frequencies are computed in parallel using:

`ProcessPoolExecutor`

This significantly improves performance on large corpora.

---

## 🔹 3. Deterministic Merge Ranking

Each merge rule is assigned a rank:

`merges[(token1, token2)] = rank`

Lower rank = higher priority during encoding.

This guarantees consistent tokenization.

---

## 🔹 4. Encoding & Decoding

`encoded = tokenizer.encode("Hello")
decoded = tokenizer.decode(encoded)`

- Encoding applies learned merges iteratively

- Decoding reconstructs original UTF-8 text

---

## 🔹 5. Save & Load

`tokenizer.save("tokenizer.json")
tokenizer = BPETokenizer.load("tokenizer.json")`

Tokenizer state (vocab + merges) is persisted in JSON format.

---

## 🔹 6. Benchmarking

Includes built-in timing utility:

`benchmark(tokenizer, text)`

Outputs:

- Encoded token length

- Execution time

---

# 🛠 Installation

Clone the repository:

`git clone https://github.com/K37VIN/All-about-Tokenizer.git
cd byte-level-bpe-tokenizer`

Python version:

`Python 3.8+`

No external dependencies required.

---

# ▶ Usage

## 1️⃣ Train the Tokenizer

`from tokenizer import BPETrainer, BPETokenizer, BytePreTokenizer

corpus = [
"Hello world!",
"Byte Pair Encoding is powerful."
]

trainer = BPETrainer(vocab_size=300)
trainer.train(corpus, BytePreTokenizer())

tokenizer = BPETokenizer(trainer)`

---

## 2️⃣ Encode Text

`encoded = tokenizer.encode("Hello world!")
print(encoded)`

---

## 3️⃣ Decode Tokens

`decoded = tokenizer.decode(encoded)
print(decoded)`

---

## 4️⃣ Save & Load

`tokenizer.save("tokenizer.json")
tokenizer = BPETokenizer.load("tokenizer.json")`

---

## 5️⃣ Benchmark

`benchmark(tokenizer, "This is a benchmark test.")`

---

# 🧠 Design Decisions

### Why Byte-Level BPE?

- Avoids unknown tokens

- Handles all Unicode

- Used in GPT-2 and modern LLMs

### Why Parallel Pair Counting?

- BPE training is computationally heavy

- Pair counting dominates runtime

- Parallelization improves scalability

### Why Modular Pre-Tokenizer?

- Clean separation of concerns

- Extensible architecture

- Mimics production tokenizer design

---

# 📁 Project Structure

`.
├── tokenizer.py
├── README.md

---

# 📊 Benchmark Example

Example output:

`Encoded length: 12
Time taken: 0.0021 seconds`

Performance scales with:

- Vocabulary size

- Corpus size

- Number of CPU cores

---

# 🚀 Future Improvements

Possible extensions:

- Add special tokens (BOS, EOS, PAD)

- Add batch encoding

- Add streaming tokenization

- Implement Trie-based merge acceleration

- Compare against HuggingFace tokenizers

- Add unit tests

- Package as pip-installable module

---

# 🎓 Educational Value

This project demonstrates understanding of:

- Subword tokenization algorithms

- Parallel computation in Python

- UTF-8 byte encoding

- Deterministic merge ranking

- Systems-oriented NLP engineering

This implementation goes beyond tutorial-level tokenizers and reflects real-world tokenizer design principles.

---

# 📜 License

MIT License

---

# ⭐ If You Found This Useful

Consider starring the repository.
