# Track 01: Foundations

Purpose: build the model and performance vocabulary needed for inference
acceleration.

## Topics

- decoder-only Transformer;
- attention and causal masking;
- RoPE;
- MHA, MQA, and GQA;
- RMSNorm and SwiGLU;
- autoregressive generation;
- sampling;
- KV cache shape and memory;
- FLOPs, bandwidth, and arithmetic intensity.

## Main Materials

- CS336 selected lectures;
- Hugging Face Transformers generation docs;
- tiny-llm book for inference structure.
- gpt-fast source reading after implementing your own naive and KV-cache
  generation loops.

## Exercises

- Implement a minimal generation loop.
- Add KV cache to the loop.
- Print KV cache shapes for each layer.
- Measure prefill and decode latency separately.
- Calculate model weight memory and KV cache memory.

## Notes To Write

Use [learning-note.md](../templates/learning-note.md) for:

- prefill vs decode;
- KV cache memory formula;
- attention FLOPs and memory;
- MHA vs MQA vs GQA.
