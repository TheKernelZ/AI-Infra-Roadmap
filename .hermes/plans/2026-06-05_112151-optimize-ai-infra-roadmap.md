# Optimize AI-Infra Roadmap Implementation Plan

> **For Hermes:** Use subagent-driven-development skill to implement this plan task-by-task.

**Goal:** Improve the AI-Infra-Roadmap so it becomes a job-oriented, evidence-driven learning system for China LLM inference infrastructure roles.

**Architecture:** Keep the current track/project/template structure, but add job targeting, weekly execution, measurable outputs, China-market keywords, project rubrics, and interview loops. Avoid turning the repo into a link dump; every resource should map to a deliverable.

**Tech Stack:** Markdown roadmap repo; optional Python benchmark/project code later; no dependency changes required for this documentation optimization.

---

## Current Context

Repo root: `/Users/thekernel/Code/AIProgrammer/learning-ai-infra/AI-Infra-Roadmap`

Current strengths:
- Clear focus on LLM inference acceleration.
- Good track sequence: foundations -> serving -> KV cache -> vLLM -> CUDA/Triton -> TensorRT-LLM -> distributed inference.
- Good learning loop: Concept -> Implementation -> Benchmark -> Explanation -> Notes.
- Existing project anchors: mini inference engine and vLLM benchmark lab.

Main gaps:
- Not yet explicitly optimized for China hiring keywords and role expectations.
- Tracks are topic lists, but not yet weekly execution plans.
- Projects lack implementation specs, artifact checklist, and scoring rubric.
- Interview guide lacks answer templates and Chinese resume bullet mapping.
- No progress tracker / portfolio readiness checklist.
- Resources do not include China-relevant inference stacks such as SGLang, LMDeploy, LightLLM, FastDeploy, ModelScope/OpenCompass ecosystem.
- No explicit “minimum viable hireable portfolio” definition.

---

## Proposed Improvement Themes

1. Add China job-market alignment.
2. Add a 12-week/24-week execution plan.
3. Convert each track from “what to study” into “what to produce.”
4. Add project rubrics and portfolio acceptance criteria.
5. Add interview answer templates in English + Chinese.
6. Add a progress tracker.
7. Add source-reading templates for vLLM/TensorRT-LLM.
8. Add benchmark methodology and result schema.

---

## Task 1: Add China Job Targeting Page

**Objective:** Make the roadmap explicitly useful for China inference AI-infra job hunting.

**Files:**
- Create: `jobs/china-inference-ai-infra.md`
- Modify: `README.md`

**Content to add:**

Create `jobs/china-inference-ai-infra.md` with sections:
- Target roles:
  - 大模型推理优化工程师
  - 大模型系统工程师
  - AI Infra Engineer
  - 推理引擎工程师
  - CUDA/Triton 优化工程师
  - 模型部署工程师
- Keyword matrix:
  - vLLM, TensorRT-LLM, SGLang, LMDeploy, LightLLM
  - KV Cache, PagedAttention, Continuous Batching
  - Speculative Decoding, Prefix Cache, Chunked Prefill
  - FP8/INT8/INT4, AWQ/GPTQ
  - CUDA, Triton, NCCL, Tensor Parallelism
  - TTFT, TPOT, P99, throughput, GPU memory
- Company-style expectations:
  - Can benchmark and explain serving behavior.
  - Can read inference engine source code.
  - Can debug latency/throughput/memory bottlenecks.
  - Can communicate tradeoffs in Chinese.
- Resume bullet examples in Chinese and English.

Modify `README.md` Start Here section to include:
- `jobs/china-inference-ai-infra.md`

**Verification:**
- Open `README.md` and verify the job page appears before the roadmap.
- Check all links are relative and valid.

---

## Task 2: Add a 12-Week Execution Plan

**Objective:** Turn the roadmap into a weekly schedule with concrete deliverables.

**Files:**
- Create: `roadmaps/12-week-inference-job-plan.md`
- Modify: `README.md`

**Plan outline:**

Week 1: Inference orientation
- Deliverable: notes on TTFT/TPOT/KV cache/prefill/decode.

Week 2: Minimal generation loop
- Deliverable: naive generation + timing script.

Week 3: KV cache implementation
- Deliverable: KV-cache generation + memory formula report.

Week 4: Batched decode and scheduler
- Deliverable: mini batch scheduler simulation.

Week 5: Serving benchmark methodology
- Deliverable: benchmark schema and first results.

Week 6: vLLM baseline benchmark
- Deliverable: vLLM report with concurrency/prompt/output sweep.

Week 7: vLLM source reading
- Deliverable: request lifecycle diagram and scheduler notes.

Week 8: KV cache system project
- Deliverable: block manager simulator and fragmentation analysis.

Week 9: CUDA basics
- Deliverable: vector add/reduction/transpose notes.

Week 10: Triton inference kernel
- Deliverable: RMSNorm or RoPE benchmark.

Week 11: TensorRT-LLM and quantization overview
- Deliverable: vLLM vs TensorRT-LLM comparison.

Week 12: Interview and portfolio packaging
- Deliverable: README polish, resume bullets, mock interview answers.

**Verification:**
- Each week has a measurable artifact.
- Each artifact maps to one job skill or interview topic.

---

## Task 3: Add Progress Tracker

**Objective:** Make progress visible and prevent passive reading.

**Files:**
- Create: `progress/README.md`
- Create: `progress/checklist.md`

**Checklist categories:**
- Core concepts
- Mini inference engine milestones
- vLLM benchmark milestones
- KV cache simulator milestones
- CUDA/Triton milestones
- TensorRT-LLM/distributed inference milestones
- Interview readiness
- Portfolio readiness

**Example checklist item format:**

```markdown
- [ ] Explain prefill vs decode in 3 minutes.
  - Evidence: `notes/prefill-vs-decode.md`
  - Interview risk if missing: high
```

**Verification:**
- Every major roadmap item has an evidence path.
- No checklist item is “read X” without output.

---

## Task 4: Strengthen Project Specs

**Objective:** Make projects implementable and portfolio-grade.

**Files:**
- Modify: `projects/mini-inference-engine.md`
- Modify: `projects/vllm-benchmark-lab.md`
- Create: `projects/kv-cache-manager.md`
- Create: `projects/cuda-triton-kernel-lab.md`
- Create: `projects/pd-disaggregation-design.md`
- Modify: `projects/README.md`

**For each project add:**
- Goal
- Why this matters for hiring
- Milestones
- Required metrics
- Expected repo artifacts
- Interview story
- Stretch goals
- Acceptance criteria

**Minimum acceptance examples:**

Mini inference engine:
- Has naive generation.
- Has KV cache generation.
- Reports prefill/decode latency separately.
- Reports KV cache memory.
- Has a short bottleneck analysis.

vLLM benchmark lab:
- Runs at least 3 controlled benchmark sweeps.
- Reports TTFT, TPOT, throughput, P95/P99, GPU memory.
- Explains tradeoff between throughput and tail latency.

KV cache manager:
- Implements contiguous allocation and block allocation.
- Reports fragmentation and cache hit rate.
- Explains when prefix caching helps.

**Verification:**
- `projects/README.md` links to all project specs.
- Each project has acceptance criteria that can be checked objectively.

---

## Task 5: Upgrade Templates

**Objective:** Make notes, source reading, and benchmark reports consistent.

**Files:**
- Modify: `templates/learning-note.md`
- Modify: `templates/experiment-report.md`
- Modify: `templates/source-reading.md`
- Create: `templates/interview-answer.md`
- Create: `templates/resume-project-bullets.md`

**Learning note improvements:**
Add:
- One-sentence interview answer
- Chinese explanation
- Formula section
- Common misconception
- Related source files / papers

**Experiment report improvements:**
Add:
- Hardware/software environment
- Model and tokenizer
- Dataset/workload shape
- Exact command
- Config table
- Raw metrics
- Observations
- Bottleneck hypothesis
- Next experiment

**Source reading improvements:**
Add:
- Entry point
- Call path
- Important classes/functions
- State transitions
- Data structures
- Open questions

**Verification:**
- Templates encourage evidence and reproducibility.
- Templates support Chinese interview preparation.

---

## Task 6: Expand Interview Guide

**Objective:** Convert interview prep from topic list into answer practice.

**Files:**
- Modify: `interview/README.md`
- Create: `interview/kv-cache.md`
- Create: `interview/serving-scheduler.md`
- Create: `interview/vllm.md`
- Create: `interview/cuda-triton.md`
- Create: `interview/distributed-inference.md`
- Create: `interview/resume-bullets.md`

**Each topic file should include:**
- Core questions
- 1-minute answer
- Deep answer
- Diagram prompt
- Common follow-ups
- Chinese phrasing
- Project evidence to cite

**Verification:**
- For every major concept in `interview/README.md`, there is at least one answer template.

---

## Task 7: Improve Resources Without Becoming a Link Dump

**Objective:** Add important China-relevant systems while preserving focus.

**Files:**
- Modify: `resources/README.md`

**Add sections:**
- Inference engines:
  - vLLM
  - TensorRT-LLM
  - SGLang
  - LMDeploy
  - LightLLM
  - Hugging Face TGI
- Benchmark/eval tools:
  - GenAI-Perf
  - vLLM benchmark scripts
  - OpenCompass, if relevant for China ecosystem
- Deployment ecosystem:
  - Kubernetes basics
  - Ray Serve
  - Docker/NVIDIA Container Toolkit
- China ecosystem notes:
  - ModelScope
  - Qwen models
  - InternLM/LMDeploy

**Rule:** For every resource, add “Use it for:” and “Expected output:” fields.

**Verification:**
- No resource is listed without a reason and deliverable.

---

## Task 8: Add Portfolio Readiness Definition

**Objective:** Define when the repo is strong enough to apply for jobs.

**Files:**
- Create: `portfolio/README.md`
- Create: `portfolio/minimum-viable-portfolio.md`

**Minimum viable portfolio:**
- 2 completed implementation projects.
- 1 benchmark report with charts/tables.
- 1 source reading document for vLLM.
- 1 Chinese technical article or long-form note.
- 20 interview answers drafted.
- Resume bullets in Chinese and English.

**Verification:**
- The roadmap has a clear transition from learning to job applications.

---

## Task 9: Add Repo Quality Checks

**Objective:** Make docs maintainable.

**Files:**
- Create: `CONTRIBUTING.md`
- Create: `.markdownlint.json` optional

**Checks:**
- Links are relative.
- Every track has exercises and exit criteria.
- Every project has acceptance criteria.
- Every resource maps to output.

**Verification commands:**

```bash
git status --short
python - <<'PY'
from pathlib import Path
for p in Path('.').rglob('*.md'):
    text = p.read_text()
    assert '\t' not in text, p
print('markdown basic check passed')
PY
```

---

## Suggested Implementation Order

1. Add `jobs/china-inference-ai-infra.md`.
2. Add `roadmaps/12-week-inference-job-plan.md`.
3. Add `progress/checklist.md`.
4. Strengthen `projects/*`.
5. Upgrade `templates/*`.
6. Expand `interview/*`.
7. Update `resources/README.md`.
8. Add `portfolio/*`.
9. Add quality checks.

---

## Risks and Tradeoffs

- Risk: Too much documentation and not enough implementation.
  - Mitigation: Every item must require an artifact.

- Risk: Roadmap becomes too broad.
  - Mitigation: Keep inference acceleration as the center; CUDA, distributed systems, and deployment are supporting skills.

- Risk: China job focus becomes superficial.
  - Mitigation: Add Chinese role names, resume bullets, interview phrasing, and China-relevant systems.

- Risk: No GPU access.
  - Mitigation: Split tasks into CPU/simulation, local small-model, and GPU-required sections.

---

## Final Validation Criteria

The optimized roadmap is successful when a reader can answer:

1. What job is this roadmap targeting?
2. What should I do this week?
3. What artifact proves I learned this topic?
4. What project can I show an interviewer?
5. What metrics did I measure?
6. What Chinese resume bullets can I write from this work?
7. What interview questions can I now answer?
