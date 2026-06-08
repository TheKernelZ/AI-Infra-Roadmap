# Interview Guide: LLM Inference Acceleration

Use this guide for near-term interview preparation.

## Must Explain Clearly

- prefill vs decode;
- why decode is often memory-bound;
- KV cache memory calculation;
- MHA vs MQA vs GQA;
- continuous batching;
- PagedAttention;
- prefix caching;
- speculative decoding;
- chunked prefill;
- quantization basics;
- vLLM vs TensorRT-LLM;
- prefill/decode disaggregation;
- TTFT, TPOT, throughput, and P99 latency.

## System Design Prompts

- Design a vLLM-like serving engine.
- Design a KV cache manager for long-context inference.
- Design a prefill/decode disaggregated serving system.
- Design a benchmark plan for a new inference optimization.

## CUDA Basics To Prepare

- grid, block, thread, warp;
- global memory vs shared memory;
- coalesced access;
- occupancy;
- memory-bound vs compute-bound;
- why FlashAttention reduces IO;
- how to profile a kernel at a high level.

## Project Narratives

Prepare short explanations for:

- mini inference engine;
- vLLM benchmark lab;
- toy KV cache manager;
- CUDA/Triton kernel lab.

