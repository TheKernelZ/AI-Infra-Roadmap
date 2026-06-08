# Track 06: TensorRT-LLM

Purpose: understand NVIDIA's production-oriented LLM inference stack.

## Topics

- engine build;
- runtime;
- plugin mechanism;
- GPT attention;
- paged KV cache;
- in-flight batching;
- remove input padding;
- FP8, INT8, and INT4;
- multi-GPU serving;
- performance tuning.

## Main Materials

- TensorRT-LLM documentation;
- TensorRT-LLM performance tuning guide;
- TensorRT-LLM KV cache documentation.

## Exercises

- Build and run a small model.
- Compare a vLLM benchmark with a TensorRT-LLM benchmark.
- Record supported quantization paths.
- Summarize where TensorRT-LLM is more complex than vLLM and why.

## Notes To Write

- vLLM vs TensorRT-LLM tradeoffs.
- TensorRT-LLM KV cache design.
- Quantization options and when they are useful.

