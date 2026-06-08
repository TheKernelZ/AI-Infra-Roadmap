# Project: vLLM Benchmark Lab

Goal: learn inference acceleration through controlled measurements.

## Benchmark Axes

- prompt length;
- output length;
- concurrency;
- batch size;
- prefix reuse rate;
- speculative decoding settings;
- quantization settings, when available.

## Metrics

- TTFT;
- TPOT;
- throughput;
- P50/P95/P99 latency;
- GPU memory;
- GPU utilization;
- cache hit rate, when available.

## Experiments

1. Baseline serving benchmark.
2. Short prompt vs long prompt.
3. Short output vs long output.
4. Prefix caching on shared-prefix workloads.
5. Speculative decoding on low-QPS and high-QPS workloads.
6. Chunked prefill under mixed prompt lengths.

## Output

Write each experiment with [experiment-report.md](../templates/experiment-report.md).

