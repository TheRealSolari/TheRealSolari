# Hi, I'm Solari

Independent builder working on **Nebula**: a language model I'm training from scratch to run fully offline on a home PC, inside a runtime called **Nytharis** that handles safety and decides what the model is allowed to do.

## Nebula

**Done so far**
- Trained a 68M-parameter version on my own AMD RX 7600 (1.2B tokens), then post-trained it in stages: persona, refusals, a 1536-token context window, and subject-by-subject "school" lessons.
- Built a 97-billion-token training corpus across 16 subject areas (math, sciences, engineering, computing and code, history, law, humanities, psychology, business, reasoning, language arts, and more), every document byte-verified.
- Built my own 32,768-token byte-level BPE tokenizer, chosen after measuring five vocabulary sizes on held-out text.
- Wrote a bf16 PyTorch trainer for AMD MI300X.

**Next**
- A 1.06B-parameter model (22 layers, grouped-query attention) trained on the full corpus.
- Plan: benchmark on MI300X, run a 5B-token pilot, then the full 97B-token run.
- The finished model runs at home: about 2.1 GB on disk, 21-30 tokens/sec on my PC.

## How I train

- **Separate stages:** data prep at home, pretraining on a cloud GPU, then post-training at home, then local use.
- **One subject at a time:** on my small model, single-subject lessons generalized (64%-100% on held-out tests) while mixed curriculums made untrained skills worse. So each lesson trains fresh from the same base with its own held-out test, and lessons are never stacked.
- **Safety in code, not just in the model:** the runtime enforces boundaries deterministically, and no checkpoint is ever promoted automatically.

## Hardware
Ryzen 5 7600X, 32 GB RAM, AMD Radeon RX 7600 (8 GB).

## Tools
Python, PyTorch, Hugging Face `tokenizers`, llama.cpp, Windows.

## Post Note
I plan on doing many more projects after I’m done with this so stay tuned if you’re interested in more. 
