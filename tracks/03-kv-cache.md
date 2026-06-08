# Track 03: KV Cache Systems

Purpose: understand and design KV cache systems for long-context serving.

## Topics

- KV cache layout;
- KV memory formula;
- paged KV cache;
- block size tradeoffs;
- prefix caching;
- cache eviction;
- KV offload;
- KV quantization;
- KV compression;
- KV transfer in prefill/decode disaggregation.

## Main Materials

- vLLM PagedAttention paper;
- vLLM prefix caching docs;
- TensorRT-LLM KV cache docs;
- LMCache.

## Exercises

- Implement a toy block allocator.
- Add block reuse for shared prefixes.
- Add LRU eviction.
- Track cache hit rate and memory usage.
- Simulate GPU-to-CPU offload.

## Notes To Write

- Why KV cache becomes the main bottleneck for long context.
- How PagedAttention differs from contiguous KV allocation.
- When prefix caching helps and when it does not.
- How MQA/GQA reduce KV memory.

