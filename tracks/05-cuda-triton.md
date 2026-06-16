# Track 05: CUDA and Triton

Purpose: build enough GPU knowledge to profile inference kernels and implement
small kernels.

This track assumes CUDA starts from zero.

## Learning Order

1. GPU execution model: grid, block, thread, warp.
2. Memory hierarchy: global, shared, register, L2, HBM.
3. Coalesced memory access.
4. Occupancy and warp stalls.
5. Nsight Systems and Nsight Compute.
6. Triton programming basics.
7. Inference-related kernels.

## Main Materials

- GPU MODE lectures;
- CUDA C++ Programming Guide;
- Programming Massively Parallel Processors;
- Triton tutorials;
- How to Scale Your Model for roofline thinking, attention IO, and parallelism
  intuition.

## Exercises

- vector add;
- reduction;
- matrix transpose;
- RMSNorm or LayerNorm;
- RoPE;
- naive attention;
- Triton matmul or RMSNorm.

## Notes To Write

- CUDA execution model.
- Global vs shared memory.
- Occupancy is useful but not the only goal.
- Why attention optimization is often about IO.
- How to read a simple Nsight Compute report.
