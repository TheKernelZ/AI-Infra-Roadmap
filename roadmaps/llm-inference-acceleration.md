# LLM Inference Acceleration Roadmap

This roadmap is designed for an LLM inference acceleration role. The target is
not only to know the terms, but to build enough system intuition to diagnose
latency, throughput, memory, and scheduling bottlenecks.

## Level 0: Orientation

Time: 1 week

Goal: build a quick mental model of LLM serving.

Learn:

- autoregressive generation;
- prefill and decode;
- KV cache;
- continuous batching;
- latency vs throughput;
- quantization basics.

Primary material:

- DeepLearning.AI: Efficiently Serving LLMs

Exit criteria:

- Explain TTFT, TPOT, throughput, and P99 latency.
- Explain why decode is often memory-bound.
- Explain why KV cache matters for long context and high concurrency.

## Level 1: Inference Foundations

Time: 2-4 weeks

Goal: understand what a decoder-only LLM computes during inference.

Learn:

- Transformer decoder block;
- attention, RoPE, GQA, RMSNorm, MLP/SwiGLU;
- sampling: greedy, top-k, top-p, temperature;
- KV cache shapes and memory formula;
- FLOPs, memory bandwidth, arithmetic intensity.

Primary materials:

- CS336 selected lectures;
- tiny-llm book, used for structure rather than MLX expertise;
- Hugging Face generation and cache documentation.

Build:

- a minimal generation loop;
- a KV-cache-enabled generation loop;
- a script that reports prefill time, decode time, and KV memory.

Exit criteria:

- Calculate KV cache memory for a given model, batch size, and sequence length.
- Describe why prefill and decode have different performance profiles.
- Draw the data flow of one generated token.

## Level 2: Serving Systems

Time: 6-8 weeks

Goal: understand how an inference engine turns many dynamic requests into GPU
work.

Learn:

- request lifecycle;
- scheduler;
- static batching vs continuous batching;
- chunked prefill;
- PagedAttention;
- prefix caching;
- speculative decoding;
- serving metrics and benchmark design.

Primary materials:

- CMU 11-868 Large Language Model Systems;
- vLLM documentation;
- vLLM PagedAttention paper.

Build:

- a toy scheduler;
- batch decode;
- a simple continuous batching loop;
- a vLLM benchmark report.

Exit criteria:

- Explain how continuous batching increases throughput.
- Explain how PagedAttention reduces KV memory fragmentation.
- Explain which workloads benefit from prefix caching or speculative decoding.

## Level 3: KV Cache Systems

Time: 4-6 weeks

Goal: treat KV cache as a first-class system component.

Learn:

- contiguous KV cache vs paged KV cache;
- block allocation and free;
- prefix reuse;
- cache eviction;
- KV offload;
- KV quantization and compression;
- KV transfer in prefill/decode disaggregation.

Build:

- a toy KV block manager;
- a prefix cache with block-level hashing;
- LRU eviction and hit-rate reporting;
- a mock GPU/CPU offload simulation.

Exit criteria:

- Design a KV cache manager for long-context serving.
- Explain the tradeoff between reuse, fragmentation, offload, and latency.
- Explain how MHA, MQA, and GQA affect KV memory.

## Level 4: GPU and Kernel Basics

Time: 6-10 weeks

Goal: become able to read kernel discussions and write simple CUDA/Triton
kernels.

Learn:

- CUDA grid, block, thread, and warp;
- global, shared, register, L2, and HBM memory;
- coalesced access;
- occupancy;
- warp divergence;
- tensor cores;
- Nsight Systems and Nsight Compute;
- Triton basics.

Primary materials:

- GPU MODE lectures;
- CUDA C++ Programming Guide as a reference;
- Programming Massively Parallel Processors as a textbook.

Build:

- vector add;
- reduction;
- matrix transpose;
- RMSNorm or LayerNorm kernel;
- RoPE kernel;
- naive attention;
- Triton matmul or RMSNorm.

Exit criteria:

- Use a profiler to distinguish memory-bound and compute-bound kernels.
- Explain why FlashAttention reduces HBM traffic.
- Write and benchmark at least one simple inference-related kernel.

## Level 5: Production Inference Stack

Time: long-term

Goal: understand production-grade inference engines and distributed serving.

Learn:

- TensorRT-LLM engine build and runtime;
- GPT attention plugin;
- paged KV cache;
- in-flight batching;
- FP8, INT8, INT4;
- tensor parallelism and pipeline parallelism;
- NCCL and RDMA basics;
- prefill/decode disaggregation;
- KV-aware routing;
- multi-node serving.

Primary materials:

- TensorRT-LLM documentation;
- tiny-vllm;
- LMCache;
- Dynamo;
- DistServe and related papers.

Build:

- TensorRT-LLM benchmark notes;
- vLLM vs TensorRT-LLM comparison;
- a design document for disaggregated prefill/decode serving.

Exit criteria:

- Explain when to choose vLLM vs TensorRT-LLM.
- Design a serving architecture with router, prefill pool, decode pool, and KV
  transfer.
- Explain the main sources of P99 latency in distributed inference.

