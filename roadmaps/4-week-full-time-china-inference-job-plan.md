# 4-Week Full-Time China Inference AI-Infra Job Plan

This is an intensive full-time plan for learning LLM inference AI infrastructure and preparing for China-focused AI infra interviews.

It assumes you can study and build for about 8-10 hours per day, 5-6 days per week.

The goal is not to master all AI infrastructure in 4 weeks. The goal is to become credible for junior-to-mid inference infrastructure interviews by producing concrete evidence:

- a mini LLM inference engine;
- a KV cache and scheduler explanation;
- a vLLM benchmark report;
- source-reading notes;
- Chinese interview answers and resume bullets.

## Target Roles

Use this plan for roles such as:

- 大模型推理优化工程师
- 大模型系统工程师
- AI Infra Engineer
- LLM Inference Engineer
- 推理引擎工程师
- 模型部署工程师
- vLLM / TensorRT-LLM 工程师
- CUDA / Triton 优化工程师

## Daily Time Budget

Recommended weekday structure:

```text
09:00-10:30  Concept learning
10:45-12:30  Implementation
13:30-15:30  Implementation / benchmark
15:45-17:00  Source reading / docs
19:00-20:30  Notes and diagrams
20:30-21:30  Interview answers / resume bullets
```

Recommended weekly rhythm:

- Monday-Thursday: learn and build.
- Friday: benchmark, write report, and polish notes.
- Saturday: mock interview, review, and catch up.
- Sunday: rest or light reading only.

## Non-Negotiable Rule

Every day must produce at least one artifact:

- code;
- benchmark result;
- diagram;
- technical note;
- interview answer;
- resume bullet;
- source-reading note.

Do not count passive reading as progress.

## Week 1: Inference Foundations and Minimal Generation

Goal: understand the inference loop deeply enough to explain prefill, decode, KV cache, and core metrics.

Main questions:

- What happens when an LLM generates one token?
- What is prefill? What is decode?
- Why does KV cache reduce repeated computation?
- Why is decode often memory-bound?
- What are TTFT, TPOT, throughput, and P99 latency?

### Day 1: Orientation and Metrics

Study:

- autoregressive generation;
- prefill vs decode;
- TTFT, TPOT, throughput, P50/P95/P99 latency;
- latency vs throughput tradeoff.

Build/write:

- Create a note: `notes/week1-prefill-decode-metrics.md`.
- Draw the request lifecycle:

```text
request -> tokenize -> prefill -> decode loop -> detokenize -> stream response
```

Interview answers:

- Explain prefill vs decode in 1 minute.
- Explain TTFT vs TPOT in 1 minute.

Exit criteria:

- You can explain why long prompts hurt TTFT.
- You can explain why long outputs hurt TPOT and total latency.

### Day 2: Transformer Decoder Inference Path

Study:

- decoder-only Transformer block;
- attention;
- RoPE;
- MHA, MQA, GQA;
- RMSNorm and SwiGLU.

Build/write:

- Create a diagram of one generated token data flow.
- Create `notes/week1-decoder-block-inference.md`.

Interview answers:

- Explain MHA vs MQA vs GQA.
- Explain why GQA reduces KV cache memory.

Exit criteria:

- You can trace tensor shapes through one decoder block at a high level.

### Day 3: Minimal Generation Loop

Build:

- Implement naive single-request generation with a small Hugging Face causal LM.
- Print per-token decode time.
- Add simple sampling options: greedy and temperature.

Suggested implementation path:

```text
experiments/mini_engine/
  generate_naive.py
  README.md
```

Measure:

- prompt length;
- output length;
- total latency;
- average per-token latency.

Write:

- `notes/week1-naive-generation.md`

Exit criteria:

- You can explain why naive generation repeats work.

### Day 4: KV Cache Generation

Build:

- Add KV-cache-enabled generation.
- Print or record KV cache shapes.
- Compare naive generation vs KV-cache generation.

Source reading, time-boxed to 2-3 hours:

- Read `gpt-fast` as a compact PyTorch reference implementation.
- Focus only on `generate.py`, `model.py`, KV cache setup, sampling, and
  `torch.compile`.
- Do not copy it before your own KV cache loop works.

Measure:

- prefill latency;
- decode latency;
- total latency;
- KV cache memory estimate.

Write:

- `notes/week1-kv-cache-generation.md`
- `source-reading/gpt-fast-generation-loop.md`

Interview answers:

- Why do we need KV cache?
- How do you estimate KV cache memory?
- What does `gpt-fast` optimize that a naive generation loop does not?

Exit criteria:

- You can write the KV cache memory formula from memory.
- You can explain why `gpt-fast` is useful for single-request generation
  latency but does not replace a serving engine such as vLLM.

### Day 5: Week 1 Benchmark Report

Build/write:

- Create a benchmark table comparing:
  - prompt length: short vs long;
  - output length: short vs long;
  - naive vs KV cache if feasible.

Create:

- `reports/week1-mini-generation-benchmark.md`

Include:

- hardware/software environment;
- model name;
- exact commands;
- metrics table;
- bottleneck analysis.

Exit criteria:

- You can explain what affects TTFT and what affects TPOT.

### Day 6: Mock Interview and Review

Prepare answers in Chinese and English:

- 什么是 prefill 和 decode？
- 为什么 decode 阶段通常是 memory-bound？
- KV Cache 的显存占用怎么计算？
- MHA/MQA/GQA 对 KV Cache 有什么影响？
- TTFT、TPOT、吞吐量、P99 延迟分别是什么意思？

Deliverable:

- `interview/week1-foundations-answers.md`

## Week 2: Serving Systems, Scheduler, and KV Cache Manager

Goal: move from single-request inference to multi-request serving intuition.

Main questions:

- Why do inference engines need schedulers?
- What is static batching vs continuous batching?
- How does a request move through a serving engine?
- Why does PagedAttention help KV memory management?

### Day 7: Request Lifecycle and OpenAI-Compatible Serving

Study:

- request lifecycle;
- streaming responses;
- OpenAI-compatible API shape;
- serving metrics.

Build/write:

- Create `notes/week2-serving-request-lifecycle.md`.
- Draw a serving system diagram:

```text
client -> HTTP server -> tokenizer -> scheduler -> model executor -> sampler -> stream output
```

Interview answers:

- Design a simple LLM serving engine.
- What metrics would you monitor in production?

### Day 8: Static Batching and Batch Decode

Build:

- Extend the mini engine or simulation to support batch decode.
- Use requests with different prompt/output lengths.

Measure:

- batch size;
- throughput;
- per-request latency;
- padding waste if applicable.

Write:

- `notes/week2-static-batching.md`

Exit criteria:

- You can explain why batching improves throughput but may hurt latency.

### Day 9: Continuous Batching Simulation

Build:

- Implement a simple continuous batching simulator.
- Model requests arriving at different times.
- Allow completed requests to leave the batch while new requests join.

Suggested files:

```text
experiments/scheduler_sim/
  continuous_batching_sim.py
  README.md
```

Report:

- throughput;
- average latency;
- P95/P99 latency;
- queue length over time.

Write:

- `notes/week2-continuous-batching.md`

Interview answers:

- How does continuous batching improve GPU utilization?
- Why can scheduling policy affect P99 latency?

### Day 10: KV Block Manager

Build:

- Implement a toy KV block manager.
- Support:
  - allocate blocks;
  - free blocks;
  - track used/free blocks;
  - report fragmentation or wasted capacity.

Suggested files:

```text
experiments/kv_cache_manager/
  block_manager.py
  test_block_manager.py
  README.md
```

Write:

- `notes/week2-kv-block-manager.md`

Interview answers:

- What problem does PagedAttention solve?
- How is paged KV cache different from contiguous KV cache?

### Day 11: Prefix Cache and Eviction

Build:

- Add a simple prefix cache simulation.
- Add LRU eviction.
- Track cache hit rate.

Measure:

- hit rate;
- memory used;
- evictions;
- saved prefill tokens.

Write:

- `reports/week2-kv-cache-manager-report.md`

Exit criteria:

- You can explain when prefix caching helps and when it does not.

### Day 12: Week 2 Mock Interview and Project Polish

Deliverables:

- Polish scheduler simulation README.
- Polish KV cache manager README.
- Create `interview/week2-serving-kv-answers.md`.

Must answer:

- 设计一个简单的大模型推理调度器。
- Static batching 和 continuous batching 有什么区别？
- PagedAttention 为什么能减少显存碎片？
- Prefix caching 适合什么业务场景？

## Week 3: vLLM Benchmarking and Source Reading

Goal: connect your toy implementation to a real production inference engine.

Main questions:

- How does vLLM process a request?
- How does vLLM scheduling work?
- How does vLLM manage KV blocks?
- How do workload shapes affect TTFT, TPOT, throughput, and P99?

### Day 13: vLLM Setup and Baseline

Study:

- vLLM documentation;
- supported models;
- OpenAI-compatible server;
- benchmark scripts.

Build/run:

- Serve a small Qwen or LLaMA-family model if GPU is available.
- If no GPU is available, read docs and prepare benchmark scripts/configs.

Report:

- `reports/week3-vllm-baseline.md`

Include:

- model;
- hardware;
- command;
- request workload;
- first metrics.

### Day 14: Workload Sweep

Benchmark axes:

- short prompt / short output;
- short prompt / long output;
- long prompt / short output;
- long prompt / long output;
- low concurrency vs high concurrency.

Metrics:

- TTFT;
- TPOT;
- throughput;
- P50/P95/P99 latency;
- GPU memory.

Deliverable:

- `reports/week3-vllm-workload-sweep.md`

Interview answers:

- Which workload is prefill-heavy?
- Which workload is decode-heavy?
- Why does concurrency improve throughput up to a point?

### Day 15: Prefix Caching and Chunked Prefill

Study/benchmark:

- prefix caching;
- chunked prefill;
- shared-prefix workloads;
- mixed prompt lengths.

Deliverable:

- `reports/week3-vllm-prefix-chunked-prefill.md`

Explain:

- when prefix caching helps;
- when chunked prefill helps;
- how these features affect TTFT and P99.

### Day 16: vLLM Source Reading: Request Lifecycle

Read source by lifecycle:

```text
request -> scheduler -> prefill/decode -> KV block allocation -> attention backend -> sampling -> output streaming
```

Deliverable:

- `source-reading/vllm-request-lifecycle.md`

Include:

- entry points;
- important classes/functions;
- state transitions;
- open questions.

Exit criteria:

- You can explain the request lifecycle without reading notes.

### Day 17: vLLM Source Reading: Scheduler and KV Cache

Focus:

- scheduler decisions;
- sequence/request state;
- KV block allocation;
- prefix cache integration.

Deliverable:

- `source-reading/vllm-scheduler-kv-cache.md`

Interview answers:

- How would you design a vLLM-like scheduler?
- What causes head-of-line blocking?
- How does KV block allocation affect memory efficiency?

### Day 18: Week 3 Mock Interview and Report Polish

Deliverables:

- One polished vLLM benchmark report.
- One vLLM architecture diagram.
- `interview/week3-vllm-answers.md`

Must answer:

- vLLM 的核心优化是什么？
- PagedAttention 解决了什么问题？
- Continuous batching 和 PagedAttention 如何配合？
- 如何设计一个 benchmark 来验证推理优化是否有效？

## Week 4: CUDA/Triton Basics, Production Stack, and Job Application Package

Goal: become interview-ready and package evidence for China job applications.

Main questions:

- What GPU basics matter for inference?
- What is memory-bound vs compute-bound?
- Why does FlashAttention reduce HBM traffic?
- When should you use vLLM vs TensorRT-LLM?
- How do you present your projects to recruiters and interviewers?

### Day 19: CUDA Execution and Memory Model

Study:

- grid, block, thread, warp;
- global/shared/register memory;
- HBM bandwidth;
- coalesced memory access;
- occupancy.

Build/write:

- Implement or study vector add and reduction.
- Create `notes/week4-cuda-execution-memory.md`.

Interview answers:

- 什么是 warp？
- global memory 和 shared memory 有什么区别？
- 什么是 memory coalescing？

### Day 20: Triton Inference Kernel

Build:

- Implement or study a simple Triton RMSNorm or RoPE kernel.
- Compare with PyTorch baseline if possible.

Deliverable:

- `reports/week4-triton-rmsnorm-or-rope.md`

Explain:

- memory reads/writes;
- expected bottleneck;
- why kernel fusion can help.

### Day 21: FlashAttention and IO-Aware Thinking

Study:

- why attention is expensive;
- HBM traffic;
- tiling;
- FlashAttention high-level idea.

Deliverable:

- `notes/week4-flashattention-io-aware-attention.md`

Interview answers:

- Why does FlashAttention reduce memory IO?
- Why is attention optimization not only about FLOPs?

### Day 22: TensorRT-LLM, Quantization, and China Inference Engines

Study:

- TensorRT-LLM;
- FP8/INT8/INT4;
- AWQ/GPTQ basics;
- `gpt-fast` int8/int4 and speculative decoding as a compact source reference;
- SGLang;
- LMDeploy;
- LightLLM;
- Qwen/ModelScope ecosystem.

Deliverable:

- `notes/week4-production-inference-stack.md`

Compare:

```text
vLLM vs TensorRT-LLM vs SGLang vs LMDeploy
```

Keep `gpt-fast` separate from this comparison: use it as a PyTorch-native
generation and optimization reference, not as a production serving framework.

Interview answers:

- When would you choose vLLM?
- When would you choose TensorRT-LLM?
- What tradeoffs does quantization introduce?

### Day 23: Distributed Inference and P/D Disaggregation

Study:

- tensor parallelism;
- pipeline parallelism;
- NCCL basics;
- prefill/decode disaggregation;
- KV transfer;
- KV-aware routing.

Deliverable:

- `design/week4-prefill-decode-disaggregation.md`

Design diagram:

```text
router -> prefill pool -> KV transfer -> decode pool -> streaming response
```

Interview answers:

- Why separate prefill and decode?
- What makes KV transfer expensive?
- What causes P99 latency in distributed inference?

### Day 24: Job Package and Mock Interview

Create final job artifacts:

- `portfolio/README.md`
- `portfolio/china-resume-bullets.md`
- `portfolio/project-narratives.md`
- `interview/final-20-questions.md`

Minimum resume bullets in Chinese:

```text
实现了一个简化版 LLM 推理引擎，支持 KV Cache、批量 Decode 和连续批处理，并基于 TTFT、TPOT、吞吐量分析不同请求模式下的性能表现。

构建了 vLLM Benchmark Lab，对不同并发、输入长度、输出长度和缓存配置进行测试，分析吞吐、P99 延迟和显存占用之间的 trade-off。

实现了 KV Cache Block Manager 模拟器，支持块分配、Prefix 复用、LRU 淘汰和碎片率分析，用于理解 PagedAttention 类系统的内存管理机制。
```

Minimum resume bullets in English:

```text
Implemented a mini LLM inference engine with KV cache, batched decode, and continuous batching; measured TTFT, TPOT, throughput, and KV memory under different workload patterns.

Built a vLLM Benchmark Lab to evaluate latency, throughput, P99, and GPU memory across concurrency, prompt length, output length, and caching configurations.

Implemented a toy KV cache block manager with block allocation, prefix reuse, LRU eviction, and fragmentation analysis to understand PagedAttention-style memory management.
```

Final mock interview topics:

- prefill vs decode;
- KV cache memory formula;
- continuous batching;
- PagedAttention;
- prefix caching;
- speculative decoding;
- vLLM architecture;
- benchmark design;
- CUDA memory hierarchy;
- FlashAttention;
- quantization;
- TensorRT-LLM vs vLLM;
- prefill/decode disaggregation.

## Final 4-Week Deliverables

By the end of 4 weeks, the repo should contain:

```text
experiments/mini_engine/
experiments/scheduler_sim/
experiments/kv_cache_manager/
reports/week1-mini-generation-benchmark.md
reports/week2-kv-cache-manager-report.md
reports/week3-vllm-workload-sweep.md
reports/week3-vllm-prefix-chunked-prefill.md
reports/week4-triton-rmsnorm-or-rope.md
source-reading/gpt-fast-generation-loop.md
source-reading/vllm-request-lifecycle.md
source-reading/vllm-scheduler-kv-cache.md
design/week4-prefill-decode-disaggregation.md
interview/week1-foundations-answers.md
interview/week2-serving-kv-answers.md
interview/week3-vllm-answers.md
interview/final-20-questions.md
portfolio/china-resume-bullets.md
portfolio/project-narratives.md
```

## Minimum Viable Job-Ready Standard

You are ready to start applying if you can:

- explain prefill/decode/KV cache clearly in Chinese;
- calculate KV cache memory for a given model shape;
- show code for a mini generation loop with KV cache;
- explain static batching vs continuous batching;
- explain PagedAttention and prefix caching;
- show at least one vLLM benchmark report;
- explain TTFT, TPOT, throughput, and P99 from your own measurements;
- walk through the vLLM request lifecycle;
- explain CUDA memory hierarchy at a high level;
- explain vLLM vs TensorRT-LLM tradeoffs;
- present 2-3 polished project stories on your resume.

## If You Have No GPU

Do not stop. Use this fallback path:

- build the mini engine on CPU with a tiny model;
- run scheduler and KV cache simulations locally;
- prepare vLLM benchmark configs and read source;
- use cloud GPU for 1-2 short benchmark sessions if possible;
- focus on reports, diagrams, and interview explanations.

CPU/simulation artifacts are still useful if the explanations are strong.

## Weekly Review Checklist

At the end of each week, answer:

- What did I build?
- What did I measure?
- What bottleneck did I understand better?
- What interview question can I now answer?
- What resume bullet can this become?
- What is still weak?

## Application Strategy During the 4 Weeks

Week 1:

- Collect 20 job descriptions from Boss直聘, 猎聘, Moka, company career pages, or LinkedIn.
- Extract repeated keywords.

Week 2:

- Start rewriting resume project bullets.
- Identify gaps between job descriptions and your evidence.

Week 3:

- Message engineers/recruiters with a concise project-based intro.
- Start applying to roles where you match 40-60% of requirements.

Week 4:

- Apply seriously.
- Use your benchmark reports and project READMEs as proof.
- Practice explaining every project in Chinese.

## Priority If Time Is Limited

If you fall behind, protect these deliverables first:

1. Mini inference engine with KV cache.
2. KV cache memory formula and explanation.
3. Continuous batching simulation.
4. `gpt-fast` source-reading note for the generation loop.
5. vLLM benchmark report or source-reading report.
6. Chinese interview answers.
7. Chinese resume bullets.

These have the highest job-search return.
