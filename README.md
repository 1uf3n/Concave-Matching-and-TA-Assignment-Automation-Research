# Concave-Matching-and-TA-Assignment-Automation-Research

## Project Overview

This repository contains code, datasets, and exploratory notebooks developed for the **Washington Experimental Mathematics Lab (WXML)** project *Matching Points in the Concave Setting*.
The work has two parallel components:

1. **Concave Matching Research**
   We study how different matching algorithms behave under concave cost functions (where classical optimal transport methods break down). Using Python simulations, we compare Greedy, Dyck, Optimal, and hybrid algorithms, and explore geometric structure, non-crossing behavior, and performance across point distributions.

2. **Automated TA/Grader Assignment for UW Math Department**
   Using real assignment requests, time schedules, and course requirements, we design a Python-based optimization engine to automate TA-to-section assignments while enforcing departmental rules described in *The Rules.pdf* .
   The system improves scalability, fairness, and efficiency compared to the manual process.

---

## 1. Concave Matching Research

### Key Points

* Implemented **Greedy**, **Dyck**, **Optimal**, **k-Greedy**, and **hybrid** algorithms.
* Ran thousands of simulations to study behavior under concave cost:
  cost = |x − y|ᵖ for 0 < p < 1.
* Visualized structures using circle diagrams, McCann circles, and Brownian-bridge–style sampling.
* Investigated:

  * when Greedy becomes optimal as $p \to 0$,
  * when Dyck becomes optimal as $p \to 1$,
  * how hybrid strategies outperform each individually,
  * how point density and distribution influence performance.
* Explored questions raised in WXML meeting notes, including switching thresholds, monotonicity failures, and geometric heuristics from *Meeting Notes.pdf* .

---

## 2. TA/Grader Assignment Optimization

### Key Points

* Built a Python solver using:

  * **Assignment Requests.csv** (preferences, time conflicts),
  * **TA Assignment Data.csv** (historical matches),
  * **Time schedule.csv** (quiz section times),
  * **Courses.csv** (course requirements).
* Implemented core constraints from *The Rules.pdf* , including:

  * TAs must cover *exactly two* 100-level quiz sections under the same lecture letter.
  * First-year and second-year TA restrictions override preferences/conflicts.
  * Professor-requested placements are hard constraints.
  * Upper-division grading uses seniority and content preferences.
* Developed multiple algorithmic formulations:

  * weighted bipartite matching,
  * greedy heuristics with time-conflict filtering,
  * Gale–Shapley variants with indifference,
  * SDP-based optimization,
  * local-swap improvement heuristics.
* Created visualizations comparing algorithmic assignments vs. official departmental matches.

---

## Repository Contents

### Data

* `Assignment Requests.csv`
* `TA Assignment Data.csv`
* `Time schedule.csv`
* `Courses.csv`

### Matching Algorithms & Simulations

* `matching.ipynb`
* `various_matchings.ipynb`
* concave-matching simulation scripts
* Greedy, Dyck, hybrid, and k-swap implementations

### TA Assignment Engine

* `TA_matching.ipynb`
* preprocessors for cleaning raw spreadsheets
* scoring functions, conflict detection, preference weighting
* matching output visualizers

### Documentation

* **The Rules.pdf** (official TA assignment constraints) 
* **Meeting Notes.pdf** (meeting notes, mathematical questions, algorithmic heuristics) 

---

## Scientific and Practical Impact

This project connects **mathematical theory**, **algorithm design**, and **real-world scheduling**:

* Advances understanding of **concave optimal transport**, an underdeveloped but important regime in matching theory.
* Shows that hybrid and multi-stage algorithms can outperform classical matchings.
* Provides a scalable and fair algorithmic framework for TA assignment at UW.
* Builds reusable infrastructure for future scheduling systems and interactive interfaces.

---

## Related Theory & References

### Greedy Matching in Optimal Transport with Concave Cost

This project is grounded in recent theoretical progress on concave-cost matching, especially the 2025 paper *Greedy Matching in Optimal Transport with Concave Cost* by Ottolini & Steinerberger .

Key ideas relevant to this repository include:

* **Concave cost functions** $c(x,y)=|x-y|^p$ for $0<p<1$ fundamentally change optimal transport geometry.
* For strongly concave settings $p \to 0$, **Greedy** matching becomes remarkably close to optimal—both theoretically and empirically.
* **Dyck matching** acts as the complementary model, becoming near-optimal for $p \to 1$.
* The paper establishes **non-crossing structure**, **random point asymptotics**, and **sharp bounds on greedy performance**, giving theoretical backing to the algorithms explored in this repo.
* In the extreme concave limit, greedy matching asymptotically recovers optimal behavior, supporting the simulations and experiments implemented here.

This repository includes implementations and experiments that visually reproduce many of the qualitative phenomena shown in the paper (e.g., McCann-circle diagrams, switching behavior of Greedy vs. Dyck vs. Optimal as concavity changes).

---

### Conformal Prediction for Matching & Assignment

We also incorporate ideas from conformal prediction as presented in *Conformal Prediction.pdf* .

While concave matching focuses on structural optimal transport behavior, conformal prediction adds a complementary perspective:

* **Distribution-free uncertainty quantification**
  Useful when evaluating the reliability of matchings or assignments generated from noisy or incomplete data.
* **Set-valued predictions**
  These can be interpreted as *allowed assignment ranges* when TA preferences or availability are uncertain.
* **Calibration and validity guarantees**
  Offering principled confidence intervals for model outputs used in assignment scoring or heuristic evaluation.

In the TA-assignment portion of the project, conformal prediction methods can help quantify:

* how confident the model is about recommending a specific TA–section match,
* whether multiple matches lie within a calibrated “equally valid” set,
* robustness of assignments under perturbations of input preferences or schedule data.

This creates a more interpretable, fairness-oriented layer on top of the optimization and matching work.

---

## Contact

Washington Experimental Mathematics Lab (WXML)
**Lufan Wang**  
Email: [lufanw@uw.edu](mailto:lufanw@uw.edu)  
University of Washington
