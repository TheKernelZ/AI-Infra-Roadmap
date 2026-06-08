# Track 04: vLLM Engineering

Purpose: move from using vLLM to understanding the system decisions behind it.

## Reading Path

Read by request lifecycle:

```text
request
-> scheduler
-> prefill/decode
-> KV block allocation
-> attention backend
-> sampling
-> output streaming
```

## Topics

- engine;
- scheduler;
- sequence/request state;
- block manager;
- PagedAttention;
- prefix caching;
- speculative decoding;
- chunked prefill;
- disaggregated prefill.

## Exercises

- Serve a Qwen or LLaMA-family model with vLLM.
- Run controlled benchmarks.
- Enable prefix caching and compare hit/miss workloads.
- Enable speculative decoding and compare workload regimes.
- Draw the request lifecycle.

## Notes To Write

- vLLM architecture summary.
- Scheduler decision flow.
- KV block allocation lifecycle.
- Workload cases where vLLM optimization helps or does not help.

