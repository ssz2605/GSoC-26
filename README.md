<p align="center">
  <img src="images/img13.png" alt="Google Summer of Code" height="85">
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  <img src="images/img14.png" alt="Sugar Labs" height="85">
</p>

<h1 align="center">Music Blocks Performance</h1>

<p align="center">
  <strong>Google Summer of Code 2026 · Sugar Labs</strong>
</p>

<p align="center">
  <a href="https://github.com/sugarlabs/musicblocks">Music Blocks</a>
  ·
  <a href="https://github.com/sugarlabs/GSoC/blob/master/Ideas-2026.md#music-blocks-performance">Project Proposal</a>
  ·
  <a href="final_report.md">Final Report</a>
</p>

---

## Overview

**Music Blocks Performance** was my Google Summer of Code 2026 project with **Sugar Labs**, focused on understanding and improving the performance, responsiveness, and playback behavior of [Music Blocks](https://github.com/sugarlabs/musicblocks).

The project followed a **measurement-driven approach**: profile the system, identify actual bottlenecks, implement targeted improvements, and validate the results through repeatable benchmarks.

Rather than optimizing based on assumptions, the work focused on answering a fundamental question:

> **Where is Music Blocks actually spending its time?**

This led to investigations across the execution engine, audio scheduling, canvas rendering, main-thread responsiveness, and performance benchmarking.

---

## Project Information

| | |
|---|---|
| **Program** | Google Summer of Code 2026 |
| **Organization** | [Sugar Labs](https://sugarlabs.org) |
| **Project** | [Music Blocks Performance](https://github.com/sugarlabs/GSoC/blob/master/Ideas-2026.md#music-blocks-performance) |
| **Contributor** | [Shreya Saxena](https://github.com/ssz2605) |
| **Mentors** | [Walter Bender](https://github.com/walterbender) · [Om Santosh Suneri](https://github.com/omsuneri) |
| **Project Period** | May 26, 2026 – August 24, 2026 |

---

## What I Worked On

### Performance Profiling & Instrumentation

Built instrumentation and benchmarking infrastructure to establish reliable performance baselines and identify where runtime was actually being spent.

### Execution Engine

Profiled the Logo execution engine and investigated redundant work and scheduling behavior to determine whether interpreter execution was a significant bottleneck.

### Audio Scheduling

Investigated playback scheduling, callback latency, and cumulative synchronization drift. Reworked scheduling to use `Tone.Transport` for improved timing precision.

### Canvas Rendering

Profiled rendering performance across browsers and investigated Firefox-specific rendering behavior, including expensive `drawImage()` operations and oversized canvas buffers.

### Main-Thread Responsiveness

Used browser performance APIs and long-task instrumentation to identify periods of main-thread blocking and evaluate their impact on playback responsiveness.

### Benchmarking

Developed repeatable benchmark workflows to compare performance before and after changes under controlled conditions.

---

## Key Results

- Established a measurement-based performance profiling framework for Music Blocks.
- Determined that Logo interpreter execution accounted for only a small portion of total playback time in the tested workloads.
- Identified audio scheduling and browser rendering as more significant contributors to observed performance issues.
- Replaced `setTimeout`-based playback scheduling with `Tone.Transport` for non-zero-delay playback events.
- Reduced measured callback latency and cumulative scheduling drift in benchmarked playback scenarios.
- Identified a Firefox-specific canvas rendering bottleneck involving `drawImage()`.
- Prevented excessive internal canvas dimensions by introducing canvas size limits.
- Added automated benchmarking to make performance changes measurable and reproducible.
- Validated changes through the existing Music Blocks test suite and performance benchmarks.

---

## Performance Investigation

The project evolved through a measurement-first workflow:

1. **Baseline & Profiling** — capture current performance characteristics before making any changes.
2. **Bottleneck Analysis** — interpret profiling data to find the real sources of slowdown.
3. **Targeted Optimization** — apply focused fixes to the bottlenecks identified.
4. **Benchmark & Validate** — re-run benchmarks to confirm the changes actually helped.
5. **Iterate & Improve** — repeat the cycle as new bottlenecks surface.
