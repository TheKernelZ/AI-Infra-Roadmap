# Resources

This file tracks the main materials used by the roadmap.

## Main Courses

- DeepLearning.AI: Efficiently Serving LLMs
- Stanford CS336: Language Modeling from Scratch
- CMU 11-868: Large Language Model Systems
- CMU Deep Learning Systems: Algorithms and Implementation

## Curated Supporting Books

Use only these two as targeted references. Do not read them cover to cover.

- How to Scale Your Model
  - Use it for: roofline thinking, matmul cost, attention IO, FlashAttention,
    tensor parallelism, and communication bottlenecks.
  - Expected output: one note connecting roofline analysis to TTFT, TPOT,
    throughput, and distributed inference.
- Build a Large Language Model From Scratch
  - Use it for: tokenizer, attention, GPT block, generation loop, and the
    conceptual bridge before writing the mini inference engine.
  - Expected output: working naive generation and KV-cache generation notes.

## Engineering References

- vLLM documentation
- TensorRT-LLM documentation
- Hugging Face Transformers generation and cache docs
- gpt-fast for a compact PyTorch-native generation, KV cache, quantization, and
  speculative decoding reference
- CUDA C++ Programming Guide
- Triton tutorials
- GPU MODE lectures

## Papers And Systems

- PagedAttention / vLLM
- FlashAttention
- Speculative Decoding
- DistServe
- SarathiServe
- LMCache
- Dynamo

## Usage Rule

Use courses for structure, docs for implementation details, and papers for
design tradeoffs. Do not turn this into an unbounded link collection.

All other books and reports are deferred unless they directly unblock a current
artifact. The priority is still code, benchmarks, source reading, and
interview-ready explanations.
