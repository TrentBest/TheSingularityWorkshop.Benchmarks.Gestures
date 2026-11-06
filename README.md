<p align="center">
  <a href="https://github.com/TrentBest/TheSingularityWorkshop.Visualize">
    <img src="https://raw.githubusercontent.com/TrentBest/TheSingularityWorkshop.Visualize/development/docs/assets/moniker.svg" alt="The Singularity Workshop" width="720" />
  </a>
</p>

# TheSingularityWorkshop.Benchmarks.Gestures

[![Benchmarks](https://github.com/TrentBest/TheSingularityWorkshop.Benchmarks.Gestures/actions/workflows/benchmark.yml/badge.svg?branch=development)](https://github.com/TrentBest/TheSingularityWorkshop.Benchmarks.Gestures/actions/workflows/benchmark.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Last commit](https://img.shields.io/github/last-commit/TrentBest/TheSingularityWorkshop.Benchmarks.Gestures/development)](https://github.com/TrentBest/TheSingularityWorkshop.Benchmarks.Gestures/commits/development)

[![Sith Policy](assets/sith-policy.svg)](https://github.com/TrentBest/TheSingularityWorkshop.Benchmarks.Gestures/actions/workflows/sith-policy.yml)

Dedicated performance experiments for the Gestures package.


Dedicated, reproducible benchmarks for the Gesture CPU reference implementation. The initial suite is ported from the benchmark project already present in the Gestures source repository; this repository establishes an independent benchmark home without changing the package implementation.

## Experiments

| Suite | What it measures | Scale |
|---|---|---|
| ChainHierarchyBenchmarks | Full hierarchy reevaluation vs incremental no-op and leaf-change evaluation | 10, 100, 1,000 joints |
| BranchingHierarchyBenchmarks | Same comparison over a balanced branching hierarchy | 10, 100, 1,000, 10,000 joints |
| CrowdGestureEvaluationBenchmarks | Shared pose evaluation vs per-agent variation evaluation | 1,000; 10,000; 100,000; 1,000,000 agents |

Crowd variation samples are deterministic and prepared outside timed methods. This suite isolates evaluator cost; it does not measure keyed random sampling, Physics integration, rigging, or rendering. The benchmark source and its scope comments are retained from the package's existing harness.

## Run locally

Clone this repository beside the Gestures source repository:

```text
workspace/
  TheSingularityWorkshop.Benchmarks.Gestures/
  TheSingularityWorkshop.Gestures/
```

Then run:

```bash
dotnet run --project src/TheSingularityWorkshop.Benchmarks.Gestures -c Release
```

The CI workflow pins the Gestures source checkout to a commit SHA. Pushes and pull requests run Dry smoke cases for all three suites; choose the **full** profile from Actions → Gestures benchmarks → Run workflow for actual BenchmarkDotNet measurements and retained reports. Update the source pin intentionally when changing the implementation revision under test.

## Evidence rules

- BenchmarkDotNet memory diagnostics are enabled.
- Fixture creation is performed in global setup, outside timed benchmark methods.
- Compare results only across equivalent hardware, runtime, source revision, and benchmark revision.
- A performance result is not a correctness, regression, or release verdict by itself.
- These benchmarks do not imply GPU performance or rendering throughput.
- No benchmark result authorizes publishing, merging, deployment, or release.

<p align="center"><img src="https://raw.githubusercontent.com/TrentBest/FSM_API/master/Documentation/Branding/TheSingularityWorkshop.png" alt="The Singularity Workshop" width="200" /></p>
