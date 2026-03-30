GRID-SYNC AI simulates an intelligent traffic management system at a 4-junction intersection (North, South, East, West). Instead of using fixed timer-based signal cycles, it dynamically allocates green light durations based on real-time vehicle counts and junction priority weights — maximizing the number of vehicles cleared per cycle.

This project demonstrates how fundamental AI and linear algebra concepts can solve real-world urban mobility challenges

How It Works

The system follows a 4-step pipeline:

1. Sense   →   Collect vehicle counts at each junction

2. Weight  →   Apply priority multipliers (road type, emergency lanes, etc.)

3. Decide  →   Calculate urgency scores via vector multiplication

4. Act     →   Proportionally allocate green time across a 180-second cycle

Core Formula

 urgency_score[i]  = traffic_count[i] × priority_weight[i]

 green_time[i]     = (urgency_score[i] / Σ urgency_scores) × total_cycle_time

 cars_cleared[i]   = floor(green_time[i] / 1.5)   # avg 1.5s per vehicle

 AI & ML Techniques Used

This project applies several core AI and machine learning concepts:

1. 🔢 Linear Algebra — Vector Operations (NumPy)

The foundation of the decision engine is element-wise vector multiplication, a linear algebra operation that transforms raw sensor data into actionable urgency 
scores

2. 🧠 Heuristic Search — Proportional Greedy Algorithm

The green time allocation uses a proportional heuristic search strategy — a greedy approach that locally optimizes each junction without exhaustive search.

Search Space: All possible green time allocations summing to 180 seconds

Heuristic Function: h(junction) = urgency_score / total_urgency

Strategy: Proportional greedy — assigns resources proportional to need

This is functionally equivalent to a single-step greedy best-first search on a continuous allocation space, commonly used in scheduling and resource allocation problems in AI.

3. 📊 State Space Representation

The system models the traffic problem as a classical AI state-space problem:

4. ⚖️ Weighted Scoring / Feature Engineering

Priority weights simulate domain knowledge feature engineering — a critical step in supervised ML pipelines:

priority_weights = np.array([1.2, 0.9, 2.0, 1.1])

2.0 for East Junction → high-traffic arterial road (like a major highway)

0.9 for South Junction → low-priority residential lane

In a production ML system, these weights would be learned from historical data using regression or reinforcement learning rather than hand-assigned.

5. 📈 Performance Metric Evaluation
The system computes a quantitative efficiency metric analogous to model evaluation in ML:

pythonefficiency = (Σ cars_cleared / Σ total_cars) × 100

This mirrors how ML models are evaluated using metrics like accuracy, F1-score, or recall — enabling comparison between different weight configurations or algorithms.


