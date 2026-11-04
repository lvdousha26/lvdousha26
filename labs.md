# Labs & Projects

Course labs and recent side projects, each in its own repo.

## CSAPP

[csapp-labs](https://github.com/lvdousha26/csapp-labs), C

All eight CMU 15-213 labs: the C warmup (queue plus test harness), datalab bit tricks, bomblab, attacklab, cachelab (cache simulator and blocked transpose), shlab (a shell with job control), malloclab (allocator), and proxylab (a caching HTTP proxy).

## JYY-OS

[jyyos-labs](https://github.com/lvdousha26/jyyos-labs), C

Nanjing University's OS course, which walks the line from how programs run concurrently to how a program becomes an operating system: `pstree` prints the process tree, `libco` is a user-level coroutine library, `crepl` is a C interpreter, and `kernel` on top of `abstract-machine` gets a minimal kernel running on bare metal.

## CS336

[cs336-lab](https://github.com/lvdousha26/cs336-lab), Python

Stanford CS336, Language Modeling from Scratch. Writeups for all five assignments:

1. basics: BPE tokenizer, Transformer, AdamW, training loop
2. systems: Triton kernels, DDP / FSDP / tensor parallelism
3. scaling: Chinchilla fit and IsoFLOP curves
4. data: Common Crawl extraction, quality filtering, dedup
5. alignment: SFT, DPO, RLHF, plus a safety supplement

## tiny-autograd

[tiny-autograd](https://github.com/lvdousha26/tiny-autograd), C++17

An autograd engine written from scratch. A `Tensor` records the op that produced it and which nodes consumed it; `graph::backward_tree` walks the ops backwards with an explicit stack, and `graph::backward_memo` does a memoized DFS that also gets DAGs right. Ops go from matmul, transpose and softmax through GELU, SiLU, layer norm and top-k; FC and conv layers are built on top, with MNIST training, GEMM and Transformer-block demos, and a small C ABI that the repo below calls from Python.

## tiny-sparse-autoencoder

[tiny-sparse-autoencoder](https://github.com/lvdousha26/tiny-sparse-autoencoder), Python

A sparse autoencoder whose forward and backward passes run inside tiny-autograd, no PyTorch involved. Two backends share one API: the engine one (top-k or ReLU+L1, linear decoder, MSE) and an independent NumPy reference with hand-derived gradients and Adam, kept so the engine's gradients can be checked line by line. The benchmark uses a known ground-truth dictionary, so whether the features are real is a number rather than a guess.

## data-preparation-pipeline

[data-preparation-pipeline](https://github.com/lvdousha26/data-preparation-pipeline), Python

A runnable LLM pretraining data pipeline, following the CS246 guest lecture on data preparation: 12 stages from raw web pages to packed token sequences — extract, dedup at url/doc/line level, LangID, heuristic filters, decontamination, quality distillation, mixing, tokenizer, best-fit plus FIM packing, stage schedule. Each stage reads the previous `docs.jsonl` and writes its own directory with a `stats.json`, so any stage can be rerun, diffed, or ablated on its own.
