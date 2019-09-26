# Tutorial: Cache Modelling

## Table of Contents

* [Introduction](#introduction)
* [Tasks](#tasks)
  * [Instruction Cache](#instruction-cache)
  * [Data Cache](#data-cache)
  * [Victim Cache](#victim-cache)
  * [Next Block Instruction Prefetch](#next-block-instruction-prefetch)
* [Deliverables](#deliverables)

## Introduction

In this assignment you model several different cache configurations using a functional simulator as a starting point. You will learn how to measure cache miss rates for the basic cache designs described in lectures.

For all parts below, report your results for each of the four benchmarks provided to you (go, gcc, fpppp, vpr) in both bar chart and table formats.


## Tasks

### Instruction Cache

Model the following two instruction cache configurations:

1. a direct-mapped cache with 32KB capacity and 64-byte blocks;
2. a 4-way set associative cache with 32KB capacity and 32-byte blocks and LRU replacement.

Measure the instruction cache miss rates for both parts. For each part, analyze the data you collect: what insight does the data give you?


### Data Cache

Model an 8-way set-associative data cache with 32KB capacity and 64-byte blocks, assuming a writeback policy with write allocate for store instructions and LRU replacement.

Measure the miss rate for load instructions (the number of load misses divided by the number of load instructions executed) and store instructions (the number of store instruction misses divided by the number of store instructions executed). Also measure the ratio of the total number of writeback events divided by the total number of store instructions. Analyze the data you collect: what insight does the data give you?

### Victim Cache

Extend the set-associative data cache above with a 2KB fully associative victim cache with LRU replacement. Recall that a block evicted from the main cache is inserted into the victim cache, and a block that hits in the victim cache is moved to the main cache. Evaluate direct-mapped, 2-way, and 4-way configurations of the main cache, measuring the load/store miss rates of the complete system (i.e., a miss in the data cache that hits in the victim cache counts as a hit). How much does the victim cache help?

### Next Block Instruction Prefetch

Extend the set-associative instruction cache above to prefetch the next consecutive block into the instruction cache when an instruction cache access misses. That is, if there is a cache miss at address 0, you service the miss but _also_ prefetch the block starting at address 32 (since the block size is 32 bytes).

Measure the miss rate due to _actual_ instruction fetches (i.e., prefetches don't count). Also measure the prefetch success rate, i.e., the fraction of prefetched blocks that hit but would have missed without the prefetch.

## Deliverables

The following deliverables are required:

1. Modify `src/sim-safe.c` so that it implements all of the experiments in this assignment, clearly labelled. Include comments describing your data structures and strategy.

2. Modify `fpppp.csv`, `gcc.csv`, `go.csv`, and `vpr.csv`, replacing _value_ in each file with the relevant simulated measurement, to five significant digits. Numbers should be reported in decimal notation rather than percentages, i.e., 0.5 instead of 50%.

3. In `report.md`, write an analysis of all of your experiments. You should describe what optimizations helped for which benchmarks and how much, and explain _why_. This should be a text file either in plain text or Markdown format.

To submit your solution, `git commit` all of your changes and `git push` them to the GitHub Classroom server. We will take a snapshot of the repositories at the assignment deadline and use that to assign marks.

