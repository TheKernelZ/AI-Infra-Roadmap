# Track 02: Serving Systems

Purpose: understand how inference engines schedule dynamic request streams.

## Topics

- request lifecycle;
- OpenAI-compatible serving;
- streaming responses;
- static batching;
- continuous batching;
- chunked prefill;
- scheduler policies;
- latency and throughput tradeoffs;
- benchmark methodology.

## Main Materials

- CMU 11-868 Large Language Model Systems;
- vLLM documentation;
- DeepLearning.AI Efficiently Serving LLMs.

## Exercises

- Run a local serving benchmark.
- Compare low concurrency and high concurrency.
- Compare short prompt/long output vs long prompt/short output.
- Report TTFT, TPOT, throughput, GPU memory, and P99 latency.

## Notes To Write

- Why continuous batching improves throughput.
- Why batching can hurt tail latency.
- How chunked prefill changes TTFT and decode fairness.

