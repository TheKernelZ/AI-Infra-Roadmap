# Project: Mini Inference Engine

Goal: build a small inference engine that teaches the core mechanics of LLM
serving.

## Milestones

1. Naive single-request generation.
2. KV-cache-enabled generation.
3. Batch decode.
4. Simple continuous batching.
5. Paged KV cache.
6. Prefix caching.
7. Simple speculative decoding.
8. Toy prefill/decode disaggregation.

## Suggested Stack

Start with PyTorch if the target is NVIDIA. Use tiny-llm as a structural guide,
but do not spend time mastering MLX unless Apple Silicon is part of the target
environment.

## Success Criteria

- The engine can generate tokens from a small decoder-only model.
- Prefill and decode latency are measured separately.
- KV cache memory is reported.
- Batch size and sequence length affect performance in explainable ways.
- Each milestone has a short note explaining the bottleneck it addresses.

