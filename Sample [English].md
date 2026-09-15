# [Example] Project Planning Template

## Reference

- Reference Paper:
  - - [Ray-Guang Cheng and Chung-Ju Chang, "Design of a fuzzy traffic controller for ATM networks," in IEEE/ACM Transactions on Networking, vol. 4, no. 3, pp. 460-469, June 1996](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=502244)

- Prompt:

> Read this paper and briefly identify the following items.

### A1. Project Summary

In 150–300 words, describe:

- **Problem to be solved**
- **Key challenges**
- **Proposed method**
- **Expected outcomes**

### A2. System Architecture

Define the following:

- **System assumptions**
- **Environment**
- **Input parameters**
- **Output parameters**
- **Proposed control modules**

Use a **system block diagram** to clearly indicate:

- Environment
- Proposed control modules
- Input parameters
- Output parameters

---

# Basic Information

| Item | Information |
|---|---|
| Project Title | |
| Student ID / Name | |
| Git Repository / Project Link | |
| Planning Approval Date | YYYY-MM-DD (The project starts being evaluated after approval by both instructors.) |

---

# Part A. Detailed Project Planning

## A1. Project Summary

In 150–300 words, describe the following:

- **Problem to be solved:**  
  ATM networks must address two interdependent problems: **Congestion Control** and **Call Admission Control (CAC)**. Conventional approaches usually handle these two problems separately and often rely on accurate traffic statistics that may be difficult to obtain in practice.

- **Key challenges:**  
  Multimedia traffic is highly bursty, making its statistical characteristics difficult to estimate in advance. Dynamically determining appropriate congestion thresholds is challenging. Admission decisions must also be made in real time with incomplete traffic information while satisfying a QoS requirement of packet loss probability ≤ 10⁻⁵.

- **Proposed method:**  
  Design an integrated **Fuzzy Traffic Controller** consisting of three coordinated modules: a **Fuzzy Congestion Controller (FCC)**, a **Fuzzy Bandwidth Predictor (FBP)**, and a **Fuzzy Admission Controller (FAC)**. Fuzzy inference is used to handle uncertainty, while a **Genetic Algorithm (GA)** is used to optimize the membership functions and control rules automatically, reducing the need for manual parameter tuning.

- **Expected outcomes:**  
  Develop a unified control architecture that integrates congestion control and CAC. Simulation results are expected to show approximately **11% higher system utilization** than the Equivalent Capacity method and approximately **4% improvement in congestion-control performance** compared with the Two-Threshold method, while maintaining the required QoS.

---

## A2. System Architecture

Define the following components.

### System Assumptions

- Two traffic classes:
  - **Type-1:** real-time traffic, such as voice and video
  - **Type-2:** non-real-time traffic, such as data
- Each traffic class has an independent finite buffer, \(K_1\) and \(K_2\).
- The total system capacity is \(C\).
- A capacity \(C_r\) is reserved for Type-1 traffic.
- QoS requirement: packet loss probability ≤ 10⁻⁵.

### Environment

- **Customer Premises Equipment (CPE):**
  - Contains a pre-buffer.
  - Adjusts its transmission rate according to the admission and congestion-control decisions.

- **ATM Network / Switching Node:**
  - Contains output buffers and an output link.
  - Represents the location where network congestion occurs.

### Input Parameters

- \(R_p\): peak bit rate
- \(R_m\): mean bit rate
- \(T_p\): peak duration
- \(q\): queue length
- \(\Delta q\): rate of change of queue length
- \(p_l\): packet loss probability
- \(C_a\): available capacity

### Output Parameters

- \(C_e\): estimated equivalent capacity
- \(y\): congestion-control action  
  - DM / DS / NC / IS / IM
- \(z\): admission decision  
  - Accept / WA / WR / Reject

Use a [**system block diagram](https://github.com/user-attachments/assets/30afb519-a782-4b61-bb98-a345e0c9929d)** to clearly show:

- **Environment**
- **Proposed control modules**
- **Input parameters**
- **Output parameters**

The diagram should make the information flow between the environment, FCC, FBP, and FAC clear.

---

## A3. Expected Deliverables and Validation

### Validation Method

- **Experimental environment:**
  - Discrete-event computer simulation
  - Single-node ATM network
  - Total capacity: \(C = 150\) Mbps
  - Buffer sizes: \(K_1 = K_2 = 200\) cells
  - Traffic model: ON/OFF Markov sources for modeling bursty traffic

- **Software / Implementation:**
  - Custom C-based simulator
  - Genetic Algorithm implemented by the project team
  - Fuzzy inference system implemented by the project team

### Experiment Scenario 1: Congestion-Control Evaluation

- **Design:**  
  Fix the number of admitted connections and gradually increase the offered load. Measure the packet loss probability \(p_l\) and system throughput as functions of the offered load.

- **Baseline:**  
  FCC vs. Two-Threshold Method

- **Purpose:**  
  Determine whether fuzzy congestion control can maintain

  \[
  p_l \leq 10^{-5}
  \]

  under highly bursty traffic. Also evaluate whether FCC reduces congestion duration and improves recovery performance compared with the conventional fixed-threshold method.

- **Expected result:**  
  Approximately 4% improvement in congestion-control performance.

### Experiment Scenario 2: Call Admission Control Evaluation

- **Design:**  
  Simulate dynamic arrivals of new calls. The FBP estimates the equivalent capacity \(C_e\), and the FAC determines whether each new call should be admitted. Record the final number of accepted calls while the QoS requirement remains satisfied.

- **Baseline:**  
  FAC + FBP vs. Equivalent Capacity Method

- **Purpose:**  
  Determine whether the fuzzy controller can achieve higher system utilization even when accurate traffic statistics are unavailable, without violating the QoS constraint.

- **Expected result:**  
  Approximately 11% improvement in system utilization.

---

## A4. Cross-Validation

Answer the following two questions:

1. **Can the proposed contributions address the identified challenges?**
2. **Do the experimental results provide sufficient evidence that the proposed method solves the problem?**

| Validation Question | Analysis | Conclusion |
|---|---|---|
| **Can the proposed contributions address the identified challenges?** | **Challenge 1 – Bursty traffic and unknown statistics:** Fuzzy inference replaces the need for exact probability distributions with rule-based reasoning, reducing dependence on prior knowledge of ON/OFF traffic distributions. **Challenge 2 – Difficulty in dynamically setting thresholds:** GA automatically optimizes membership functions and fuzzy rules, reducing manual parameter tuning. **Challenge 3 – Difficulty in integrating congestion control and CAC:** The output \(y\) of the FCC is provided to the FAC, while the modules share information such as \(p_l\), enabling coordinated decisions within a unified architecture. | ✓ Yes |
| **Do the experimental results provide sufficient evidence that the proposed method solves the problem?** | **Scenario 1:** FCC improves congestion-control performance by approximately 4% compared with the Two-Threshold method while maintaining \(p_l \leq 10^{-5}\). This provides simulation-based evidence for the congestion-control contribution. **Scenario 2:** FAC + FBP improves system utilization by approximately 11% compared with the Equivalent Capacity method without violating the QoS requirement. This supports the CAC contribution. **Limitation:** The evaluation is based only on discrete-event simulation. No physical ATM hardware deployment or large-scale real-world evaluation is provided, and the ON/OFF Markov traffic model may not represent all real multimedia traffic characteristics. | ⚠ Partially Validated |

---

# General Template for Other Projects

When applying this template to another project, maintain the following logical flow:

**Problem → Importance → Challenges → System Block Diagram → Assumptions → Inputs/Outputs → Metrics → Experiment Design → Figures → Cross-Validation**

The final project plan should make it possible to answer three questions clearly:

1. **What problem are you trying to solve, and why is it difficult?**
2. **How does your proposed method address each identified challenge?**
3. **What experiment and metric will demonstrate that the proposed method actually solves the problem?**
