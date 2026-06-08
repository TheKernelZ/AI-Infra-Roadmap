# AI Infra Roadmap

A structured learning roadmap for AI infrastructure, with the current focus on
LLM inference acceleration.

This repository is organized around one principle:

> Learn the system by building, measuring, and explaining it.

The first roadmap targets LLM inference acceleration roles: vLLM-style serving,
KV cache systems, batching, PagedAttention, CUDA/Triton basics, TensorRT-LLM,
and distributed prefill/decode serving.

## Start Here

1. Read the main roadmap:
   - [LLM Inference Acceleration](roadmaps/llm-inference-acceleration.md)
   - [4-Week Full-Time China Inference Job Plan](roadmaps/4-week-full-time-china-inference-job-plan.md)

2. Work through the tracks in order:
   - [Foundations](tracks/01-foundations.md)
   - [Serving Systems](tracks/02-serving-systems.md)
   - [KV Cache Systems](tracks/03-kv-cache.md)
   - [vLLM Engineering](tracks/04-vllm.md)
   - [CUDA and Triton](tracks/05-cuda-triton.md)
   - [TensorRT-LLM](tracks/06-tensorrt-llm.md)
   - [Distributed Inference](tracks/07-distributed-inference.md)

3. Build project evidence:
   - [Projects](projects/README.md)
   - [Mini Inference Engine](projects/mini-inference-engine.md)
   - [vLLM Benchmark Lab](projects/vllm-benchmark-lab.md)

4. Prepare for interviews:
   - [Interview Guide](interview/README.md)

## Repository Structure

```text
AI-Infra-Roadmap/
  README.md
  roadmaps/
    llm-inference-acceleration.md
  tracks/
    01-foundations.md
    02-serving-systems.md
    03-kv-cache.md
    04-vllm.md
    05-cuda-triton.md
    06-tensorrt-llm.md
    07-distributed-inference.md
  projects/
    README.md
    mini-inference-engine.md
    vllm-benchmark-lab.md
  interview/
    README.md
  resources/
    README.md
  templates/
    learning-note.md
    experiment-report.md
    source-reading.md
```

## Learning Loop

For every topic, use the same loop:

```text
Concept -> Implementation -> Benchmark -> Explanation -> Notes
```

Do not count a topic as learned until you can:

- explain the bottleneck it solves;
- identify whether it affects TTFT, TPOT, throughput, or memory;
- run or sketch a minimal implementation;
- compare when it helps and when it does not;
- connect it to vLLM, TensorRT-LLM, or CUDA/Triton.

## Current Priority

The recommended priority is:

```text
DeepLearning.AI short course
-> CS336 selected lectures
-> tiny-llm / PyTorch mini inference engine
-> CMU 11-868 LLM Systems
-> vLLM benchmark and source reading
-> CUDA/Triton basics
-> TensorRT-LLM and distributed inference
```

