# Workload Balancer v1.0
## Functional Specification

### Project Purpose

The Workload Balancer is an operational planning system designed for housekeeping departments in hotels, resorts, and external cleaning businesses.

Its purpose is to automatically distribute daily cleaning tasks among available teams while maintaining:
- Fair workload distribution
- Operational efficiency
- Reduced walking time between work areas
- Team productivity balance
- Visibility of special cleaning requirements

The system is based on real housekeeping operations and is designed around the workflow currently used in resort environments.

---

# Core Objectives
The system must:
1. Distribute workload fairly among teams.
2. Consider differences in employee productivity.
3. Minimize unnecessary movement between stages.
4. Prioritize arrivals over departures.
5. Identify Deep Cleaning rooms.
6. Maintain balanced workloads even when demand is uneven between stages.
7. Adapt to varying staffing levels.

---

# Operational Environment
The property is divided into multiple geographical zones called:
`Stage 1`, `Stage 2`, `Stage 3`.

Characteristics:
- Stages are physically separated.
- Stage 3 is generally larger than the others.
- Walking time between stages should be minimized.
- Teams should preferably remain within one stage.
- Stage restrictions are considered soft constraints.

---

# Employee Structure
Employees belong to one of two categories: `Permanent Staff` or `Casual Staff`.

**Permanent Staff:**
- Can act as Team Leaders.
- Usually Level 2 or Level 3.
- Maximum expected Level 3 employees: 2.

**Casual Staff:**
- Usually Level 1 or Level 2.
- Cannot act as Team Leaders.

---

# Productivity Levels
Multipliers:
- Level 1: 1.0 (Base)
- Level 2: 1.2
- Level 3: 1.4

Purpose: Recognize performance differences without excessively penalizing high performers.

---

# Team Structure
- Minimum size: 2 employees.
- Maximum size: 4 employees.
- Every team MUST contain 1 Team Leader (Permanent Staff).

**Team Capacity Calculation:**
Sum of individual member multipliers.
Example: *Leader (1.4) + Casual (1.0) = 2.4 Total Capacity.*

---

# Room Structure
Each room entry includes:
- `room_number`: Unique identifier.
- `stage`: Location (1, 2, or 3).
- `room_type`: Standard, Kitchen Unit, etc.
- `category`: Arrival or Departure.
- `deep_clean`: Boolean (True/False).
- `points`: Effort value (e.g., 3, 5, 8).

---

# Work Prioritization & Logic

**Priorities:**
1. Arrivals (Priority 1)
2. Departures (Priority 2)

**Assignment Logic (Cascading):**
1. Group rooms by Stage.
2. Assign rooms to the team assigned to that Stage first.
3. If a team finishes its Stage's rooms but still has capacity, it "cascades" to help other Stages (usually Stage 3).
4. Balance workload by Points, not by room count.

---

# Success Criteria
1. Loads are balanced according to team capacity.
2. Arrivals are prioritized.
3. Deep Clean rooms are clearly marked.
4. Manual planning time is reduced.

---
**Version:** 1.0
**Author:** Daniel Martinez
