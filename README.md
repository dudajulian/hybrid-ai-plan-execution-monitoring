# Hybrid AI Plan Execution Monitoring

This repository implements a hybrid system combining Large Language Models (LLMs) and Answer Set Programming (ASP) for **plan execution monitoring**. It is part of the *Intelligent Systems* lecture/practical at \[your institution].

---

## Table of Contents

* [Motivation](#motivation)
* [Features](#features)
* [Architecture](#architecture)
* [Installation](#installation)
* [Usage](#usage)
* [Repository Structure](#repository-structure)
* [Examples](#examples)
* [Contributing](#contributing)
* [License](#license)

---

## Motivation

Plan execution monitoring is the task of checking whether a plan is being carried out correctly, detecting deviations, and inferring causes when execution does not match plan. Purely data-driven or purely formal methods each have limitations. This project explores combining LLMs (for flexibility, handling natural language and unexpected inputs) with logic-based ASP (for precise, rule-based reasoning) to get the best of both worlds.

---

## Features

* A module based on ASP for formal domain modelling and monitoring logic.
* A module using LLMs to interpret unexpected observations, ambiguous actions, or natural language descriptions.
* Hybrid reasoning: deviations detected by ASP may trigger LLM-based inference; LLM outputs are checked/validated by ASP.
* Task scripts to run experiments / exercises (e.g. `task1.py`, `task2.py`)
* Configuration for constants/domains separated (e.g. `asp_constants.py`, `llm_constants.py`)

---

## Architecture

```
+-------------------+          +-------------------+
| Observations /    |   →      | LLM Module        |
| Sensor / Log Data |          +-------------------+
|                   |                ↓
+-------------------+           Predicted Deviations,
                                 Interpreted Descriptions
        ↓                                ↓
+-------------------+         +-------------------+
| ASP Module        | ←------ | Validation / Logic|
| Formal model of   |         | Rules & Domain    |
| plan & domain     |         | Constants         |
+-------------------+
        ↓
Plan Execution Status Report / Diagnostics
```

* **ASP Module**: uses domain model in `.pl` files, constants, and module logic in `asp_module.py`.
* **LLM Module**: uses prompts, temperature/configuration in `llm_module.py` and `llm_constants.py`.
* **Translation / Interfaces**: scripts like `translate_plan.py` produce plan representations usable by ASP; `task*.py` contain example workflows.

---

## Installation

Assumes you have Python 3.8+ (or version used in the repo).

1. Clone the repository:

   ```bash
   git clone https://github.com/dudajulian/hybrid-ai-plan-execution-monitoring.git
   cd hybrid-ai-plan-execution-monitoring
   ```

2. Create a virtual environment:

   ```bash
   python -m venv venv
   source venv/bin/activate   # on Linux/Mac
   # or
   venv\Scripts\activate      # on Windows
   ```

3. Install dependencies:

   ```bash
   pip install -r pip-requirements.txt
   ```

   Or, if using conda:

   ```bash
   conda env create -f conda-requirements.txt
   conda activate <env-name>
   ```

4. You may need to install ASP solver (e.g. `clingo`) separately; ensure it’s available in path.

---

## Usage

Examples of running the system:

* Run a monitoring task:

  ```bash
  python task1.py
  ```

* Translate a plan into the input format for ASP:

  ```bash
  python translate_plan.py --input <plan_file> --output <asp_input>
  ```

* Use the LLM module directly:

  ```bash
  python llm_module.py --prompt <prompt_file> --config <config_file>
  ```

Adjust paths / domain constants as needed in configuration files.

---

## Repository Structure

| File / Folder                          | Purpose                                                       |
| -------------------------------------- | ------------------------------------------------------------- |
| `asp_domain_modelling.pl`              | Domain rules and logic in ASP.                                |
| `asp_module.py`                        | Interface to ASP solver; applies observations, logic, checks. |
| `llm_module.py`                        | Interacts with LLM, prompt management, response extraction.   |
| `asp_constants.py`, `llm_constants.py` | Configuration: constants, thresholds, domain-specific values. |
| `translate_plan.py`                    | Converts plan descriptions into ASP-consumable format.        |
| `task1.py`, `task2.py`                 | Example tasks/demonstrations.                                 |
| `answers/`                             | Solutions / expected outputs (for exercises).                 |

---

## Examples

* **Task 1**: Given a plan and observations, detect if plan execution deviates.
* **Task 2**: Use LLM to interpret ambiguous observation and feed result to ASP to decide status.

Include sample input and sample output in `answers/` for comparison.

---

## Contributing

* Document clearly what component you add (LLM prompt, logic rule, constant)
* Write tests or example runs to demonstrate correctness
* Commit with your GitHub user/email so contributions appear in history

---

## License

Apache 2.0

