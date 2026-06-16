# Track 07: Distributed Inference

Purpose: learn how low-latency serving changes at cluster scale.

## Topics

- tensor parallelism;
- pipeline parallelism;
- data-parallel serving;
- NCCL collectives;
- RDMA basics;
- router design;
- load balancing;
- prefill/decode disaggregation;
- KV transfer;
- KV-aware routing;
- autoscaling;
- multi-tenant serving.

## Main Materials

- DistServe;
- Dynamo;
- LMCache;
- vLLM disaggregated prefill documentation;
- TensorRT-LLM distributed serving documentation;
- How to Scale Your Model for tensor parallelism, network rooflines, and
  communication bottlenecks.

## Exercises

- Design a prefill/decode disaggregated architecture.
- Specify request routing and KV transfer flow.
- Define SLO metrics.
- Identify likely P99 latency sources.

## Notes To Write

- Why prefill and decode can be separated.
- What makes KV transfer expensive.
- How KV-aware routing improves cache reuse.
- How distributed inference differs from distributed training.
