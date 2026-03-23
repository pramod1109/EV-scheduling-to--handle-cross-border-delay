EV Depot Grid & Charging Optimizer
This repository contains a Pyomo-based mathematical optimization model designed to manage electric bus charging schedules. The goal is to minimize peak power demand (Grid Impact) while ensuring all buses meet their target State of Charge (SOC) before departure.

🚀 Core Features
Peak Shaving: Actively minimizes the global maximum power draw across the depot.

Dynamic SOC Targeting: * Overnight Stays (>6h): Target 95% SOC.

Short Stays: Target 80% SOC.

Soft Constraint Stability: Uses Slack variables and Penalties to ensure the solver (HiGHS) always finds a feasible solution, even during high-traffic days.

Multi-Vehicle Support: Handles varying battery capacities and charger power limits (e.g., BYD K9, Foton).
🧮 Optimization LogicObjective FunctionThe model minimizes a weighted multi-objective function:$$\text{Minimize } Z = 0.3 \cdot P_{peak} + \text{Shortfall Penalty} + \text{Missed Departure Penalty} - 0.1 \cdot \text{Total Energy}$$

Key ConstraintsPower Limit: $P_{s,t} \le \text{Max Charger Power}$Grid Limit: $\sum P_{s,t} \le \text{Depot Limit} + \text{Violation Slack}$Battery Capacity: $\text{Initial Energy} + \text{Added Energy} \le \text{Battery Capacity} \cdot 1.001$ (with float buffer).Energy Requirement: $\text{Energy Added} + \text{Slack} \ge \text{Target Energy}$.🛠️ RequirementsPython 3.10+Pyomo (pip install pyomo)HiGHS Solver (Installed via highspy or system binary)Pandas for data handling
