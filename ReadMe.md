# OPF Relaxation Benchmark

This repository provides a Julia-based framework to benchmark the performance, accuracy, and AC feasibility of various Optimal Power Flow (OPF) relaxations against the full, non-convex AC-OPF problem.

It uses the `PowerModels.jl` library to evaluate several standard formulations (DCOPF, SOC-WR, QC, SDP) on test cases from the PGLib-OPF library under stochastic load conditions.

## Description

The script performs the following steps:
1.  **Scenario Generation**: For each test case, it generates multiple load scenarios by applying random scaling factors to the base loads.
2.  **Model Evaluation**: It solves each scenario using the full ACOPF model (as a baseline) and several common relaxations.
3.  **Metrics Calculation**: It calculates key performance indicators:
    * **Solver Runtime**: How long the optimization takes.
    * **Optimality Gap**: The percentage difference in objective value compared to the ACOPF solution.
    * **AC Feasibility**: The degree to which the relaxation's solution violates voltage and branch limits when plugged back into the AC power flow equations.
4.  **Reporting**: It outputs a summary table to the console and generates a 2x2 plot visualizing the trade-offs between speed, quality, and feasibility.

## Installation

### Prerequisites
- [Julia](https://julialang.org/downloads/) (version 1.6 or later)
- The [PGLib-OPF dataset](https://github.com/power-grid-lib/pglib-opf). Download and extract it so that the `pglib-opf-master` directory is in the root of this project folder.

### Project Setup
1.  **Clone the repository:**
    ```bash
    git clone <your-repo-url>
    cd <your-repo-name>
    ```
2.  **Instantiate the Julia Environment:**
    Open the Julia REPL in the project directory and run the following commands to install all required packages.
    ```julia
    using Pkg
    Pkg.activate(".")
    Pkg.instantiate()
    ```

## Usage

You can run the analysis directly from your terminal:
```bash
julia run_analysis.jl