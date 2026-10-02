# AI Constraint Scheduler

An intelligent meeting scheduler that uses **Constraint Satisfaction Problems (CSPs)** to construct conflict-free schedules while respecting hard constraints and optimizing soft preferences.

Inspired by concepts studied in Stanford CS221: Artificial Intelligence - Principles and Techniques. This repository is an independently structured portfolio project with its own application framing, implementation, experiments, and documentation.

## Why this project?

Scheduling looks simple until multiple requirements interact:

- People have different availability.
- Meetings cannot overlap.
- Rooms have capacity limits.
- Some meetings require specific participants.
- Some time slots are preferred over others.

Instead of relying on trial-and-error rules, this project models scheduling as a **constraint satisfaction problem** and searches the solution space intelligently.

## AI formulation

**Variables**: meetings to schedule.

**Domains**: feasible `(time_slot, room)` assignments for each meeting.

**Hard constraints**:

- No participant can attend two meetings at the same time.
- A room can host at most one meeting at a time.
- Room capacity must be large enough.
- Required participants must be available.

**Soft preference**:

- Prefer earlier meeting slots when possible.

## Solver pipeline

```text
Scheduling problem
      |
      v
CSP representation
      |
      v
Backtracking search
      |
      +--> MRV variable ordering
      |
      +--> LCV value ordering
      |
      +--> Forward checking
      |
      v
Valid schedule
```

## Project structure

```text
ai-constraint-scheduler/
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
├── src/
│   ├── __init__.py
│   ├── csp.py
│   └── scheduler.py
├── examples/
│   └── demo.py
├── tests/
│   └── test_scheduler.py
└── assets/
```

## Getting started

### 1. Clone

```bash
git clone https://github.com/<your-username>/ai-constraint-scheduler.git
cd ai-constraint-scheduler
```

### 2. Install

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

On Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

### 3. Run the demo

```bash
python examples/demo.py
```

### 4. Run tests

```bash
pytest -q
```

## Example output

The demo creates a feasible schedule such as:

```text
AI Project Sync      | Mon 09:00 | Atlas Room | Alice, Bob
Design Review        | Mon 10:00 | Cedar Room | Alice, Carol
Data Science Standup | Mon 11:00 | Cedar Room | Bob, Dan
Planning             | Mon 12:00 | Atlas Room | Alice, Dan
```

The exact assignment can vary because multiple feasible schedules may exist.

## What I explored

The repository is designed to make the AI behavior measurable, not just functional. Useful experiments include:

1. Compare plain backtracking with MRV.
2. Measure how forward checking reduces dead-end exploration.
3. Increase the number of meetings and observe search growth.
4. Add soft preferences and compare solution quality.

Suggested metrics:

| Metric | Meaning |
|---|---|
| Nodes explored | Number of partial assignments examined |
| Backtracks | Number of search reversals |
| Runtime | Wall-clock solving time |
| Constraint checks | Number of consistency evaluations |
| Preference score | Quality of the final schedule |

## Key takeaway

Classical AI techniques can transform a combinatorial scheduling problem into a structured search problem. The most interesting engineering question is not only whether a solution exists, but **how intelligently the solver can navigate the search space**.

## Future improvements

- Add calendar import/export.
- Support weighted soft constraints.
- Add a web UI for interactive scheduling.
- Compare CSP search with integer programming.
- Visualize the search tree and constraint propagation.

## License

MIT
