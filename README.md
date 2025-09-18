
## Space Object Tracking Pipelines

```mermaid
flowchart TB
  %% === FUTURE COMPACT ===
  subgraph FUTURE["Tomorrow (AI/ML Future)"]
    direction TB
    A2[Ground + Space Observations] --> B2[Orbit Determination + Data Fusion]
    B2 --> C2[AI/ML Risk Inference]
    C2 --> D2[Decision Support + Optimization]
    D2 --> E2[Autonomous Maneuver + Continuous Learning]
  end

  %% === TODAY COMPACT ===
  subgraph TODAY["Today"]
    direction TB
    A1[Ground Observations] --> B1[Orbit Determination]
    B1 --> C1[TLE/Ephemeris]
    C1 --> D1[Conjunction Assessment]
    D1 --> E1[Operator Decision & Maneuver]
  end

```

### As-of Today Workflow

Currently, satellites and debris are tracked using **ground-based observations** such as radars, optical telescopes, GNSS signals, and telemetry from spacecraft. This raw tracking data is processed through **orbit determination** to estimate each object’s position and velocity in space. From here, simplified orbit models called **Two-Line Elements (TLEs)** are generated for fast predictions, while **ephemeris files** are created for high-precision trajectory modeling. 

These models are propagated forward in time to predict trajectories and checked for possible close approaches, called **conjunctions**. When a potential risk is identified, a **Conjunction Data Message (CDM)** is issued, containing details like time of closest approach, miss distance, and probability of collision. Operators then decide whether to maneuver or take no action. Once a decision is executed, the new orbit state is updated, and the cycle continues with fresh observations.  

---

### AI/ML Future Workflow

In the future, tracking expands to include both **ground-based sensors** (radar, optical, GNSS) and **space-based sensors** (crosslinks between satellites and onboard measurement systems). Ground data continues to feed **orbit determination**, while space-based inputs not only improve orbit estimation but also act as **supplementary measurements** feeding into a **multi-source data fusion layer**. This fusion provides a more complete and accurate picture of the orbital environment.  

From there, trajectories and uncertainties are processed by a **risk inference engine**, which uses AI and machine learning to forecast collision risks and rank decision options. A **decision support layer** then optimizes strategies using tools like game theory, and candidate maneuvers can be executed autonomously. After execution, a **feedback loop** records the outcome and updates the system, while a **continuous learning framework** (including reinforcement learning and supervised updates) improves the models over time.  

The AI/ML blocks—**data fusion, risk inference, decision support, autonomous execution, and continuous learning**—introduce speed, adaptability, and predictive intelligence that today’s workflow lacks.




```mermaid
flowchart TB
  %% === FUTURE PIPELINE ===
  subgraph FUTURE["Tomorrow (AI/ML Future)"]
    direction TB
    A2_GB[Ground-based Observations: Radar, Optical, GNSS] -->|Raw Tracking Data| B2[Orbit Determination]
    A2_SB[Space-based Observations: Crosslinks, Onboard Sensors] -->|Raw Tracking Data| B2[Orbit Determination]

    B2 -->|State Vector| C2[TLE Generation - for SGP4]
    B2 -->|State Vector| D2[Ephemeris Generation - OEM SPICE]

    C2 -->|Catalogs| J2[Data Fusion Layer Multi-source Sensor Fusion]
    D2 -->|Catalogs| J2
    A2_SB -->|Supplementary Measurements| J2

    J2 -->|Unified State + Covariance| E2[Propagation and Prediction Models]
    E2 -->|Trajectories + Uncertainty| K2[Risk Inference Engine ML and Probabilistic Forecasting]

    K2 -->|Risk Assessment + Ranked Options| L2[Decision Support Layer Optimization and Game Theory]
    L2 -->|Candidate Maneuver Strategy| M2[Autonomous Maneuver Execution]
    M2 -->|Executed Maneuver Data| N2[Post-Maneuver Feedback Loop]

    N2 -->|Updated State + CDM Outcomes| O2[Continuous Learning Federated RL Supervised ML]
    O2 --> J2

    K2 -.->|ML Opportunities: Supervised, Bayesian Updates, Reinforcement Learning, Graph NN| L2
  end

  %% === TODAY PIPELINE ===
  subgraph TODAY["Today"]
    direction TB
    A1[Observations: Radar, Optical, GNSS, Telemetry] -->|Raw Tracking Data| B1[Orbit Determination]
    B1 -->|State Vector| C1[TLE Generation - for SGP4]
    B1 -->|State Vector| D1[Ephemeris Generation - OEM SPICE]

    C1 -->|TLE for SGP4| E1[Propagation]
    D1 -->|High-precision Ephemeris| E1

    E1 -->|Predicted Trajectories| F1[Conjunction Assessment]
    F1 -->|Conjunction Event| G1[CDM: TCA, Miss Distance, Pc, Covariance]
    G1 -->|CDM Distributed| H1[Operator Decision]
    H1 -->|Maneuver Plan or No Action| I1[Updated Orbit State]
  end

  %% === Styling ===
  class J2,K2,L2,M2,N2,O2 new;
  classDef new fill:#ffe599,stroke:#cc9900;

```

## Comparison: Today vs AI/ML Future Pipeline

| Aspect                  | Today (As-of)                                | Tomorrow (AI/ML Future)                          |
|--------------------------|-----------------------------------------------|--------------------------------------------------|
| **Observation Sources** | Ground-based only (radar, optical, GNSS, telemetry) | Ground + space-based (crosslinks, onboard sensors) |
| **Data Processing**     | Orbit determination → TLE / Ephemeris        | Orbit determination + multi-source **data fusion** |
| **Trajectory Prediction** | Propagation with fixed models                | Propagation + AI-enhanced prediction with uncertainties |
| **Risk Assessment**     | Conjunction assessment → CDM alerts           | **Risk inference engine** with ML & probabilistic forecasting |
| **Decision Making**     | Human operators interpret CDMs and decide     | **Decision support layer** with optimization & game theory |
| **Maneuver Execution**  | Manual execution after operator approval      | **Autonomous maneuver execution** with oversight |
| **Learning**            | Static, relies on new observations only       | **Continuous learning** (supervised + RL updates) |
| **Strengths**           | Mature, trusted, human oversight              | Faster, smarter, adaptive, scales with traffic    |
| **Weaknesses**          | Slow, reactive, operator bottleneck           | Needs trust, validation, and robust AI models     |


## Technical + Strategic Layers of Collision Avoidance

### Today
- **Observations** rely on ground-based radar, optical, GNSS, and telemetry.  
- **Orbit determination** produces TLEs and ephemerides.  
- **Conjunction assessment** identifies risks.  
- **Operator decisions** are made manually, often under time pressure.  
- Strategies are limited to **preventing**, **mitigating**, or **accepting** the risk.  

### Tomorrow (AI/ML Future)
- **Observations** expand to include space-based crosslinks and onboard sensors.  
- **Data fusion** creates a unified orbital picture.  
- **AI/ML risk inference** models not only predict risks but quantify uncertainties.  
- A **decision support layer** evaluates **cost–benefit tradeoffs** of maneuvers using optimization and game theory.  
- Operators (or autonomous systems) can categorize actions into:  
  - **Prevention** (active avoidance, design choices),  
  - **Mitigation** (reduce severity),  
  - **Share/Transfer** (insurance, joint operations),  
  - **Accept** (low risk, tolerable), or  
  - **Do Nothing** (rational default).  
- Decisions feed into **autonomous maneuver execution**, with feedback loops driving **continuous learning**.  


```mermaid
flowchart TB

  %% === FUTURE COMPACT WITH STRATEGY ===
  subgraph FUTURE["Tomorrow (AI/ML Future)"]
    direction TB
    A2[Ground + Space Observations] --> B2[Orbit Determination + Data Fusion]
    B2 --> C2[AI/ML Risk Inference]
    C2 --> D2[Decision Support + Cost–Benefit Analysis]
    D2 --> E2[Strategy Category: Prevent or Mitigate or Share/Transfer or Accept or Do Nothing]
    E2 --> F2[Autonomous Maneuver + Continuous Learning]
  end


  %% === TODAY COMPACT WITH STRATEGY ===
  subgraph TODAY["Today"]
    direction TB
    A1[Ground Observations] --> B1[Orbit Determination]
    B1 --> C1[TLE/Ephemeris]
    C1 --> D1[Conjunction Assessment]
    D1 --> E1[Operator Decision]
    E1 --> F1[Manual Strategy: Prevent or Mitigate or Accept]
  end


```

# 🛰️ Game Theory in Collision Avoidance

## Why Game Theory Matters  
When two satellite operators face a close approach (conjunction), they both need to decide whether to **maneuver** or **not maneuver**. This decision is not purely technical — it involves **costs, risks, and incentives**.  
- **Maneuvering**: increases safety but consumes fuel, reduces mission lifetime, and may disrupt services.  
- **Not maneuvering**: avoids immediate costs but leaves the collision risk unresolved.  

This creates a **strategic dilemma** because the best outcome for one operator may depend on the choice of the other.

---

## Example: A Prisoner’s Dilemma in Space  
This scenario can be modeled as a **Prisoner’s Dilemma**, where each operator must choose to maneuver or not.  

### Payoff Matrix  

| Operator A \ Operator B | Maneuver                     | Not Maneuver               |
|--------------------------|------------------------------|-----------------------------|
| **Maneuver**            | (-1, -1) Safe, both pay cost | (-1, 0) A pays, B free rides |
| **Not Maneuver**        | (0, -1) A free rides, B pays | (-100, -100) Collision risk |

- **-1** → maneuver cost (fuel, service disruption)  
- **0** → no immediate cost  
- **-100** → catastrophic collision loss  

---

## Insights  

- **Short-term rationality**: Each operator wants the other to maneuver while avoiding costs themselves.  
- **Free riding problem**: If one maneuvers and the other does not, the non-maneuvering operator benefits without cost.  
- **Mutual risk**: If both refuse to maneuver, the worst outcome occurs — possible collision.  
- **Systemic issue**: Without coordination, operators may under-respond, leaving the whole system at higher risk.  

---

## Strategy Categorization & Considerations  

### 1. Prevent  
- **Goal:** Avoid risk entirely.  
- **Considerations:** Probability of collision, fuel availability, mission-critical payloads.  
- **Parameters for payout calculation:** Cost of maneuver, expected loss if collision occurs, likelihood of avoidance success.

### 2. Mitigate  
- **Goal:** Reduce likelihood or severity of impact.  
- **Considerations:** Partial orbital adjustments, shielding, operational flexibility.  
- **Parameters:** Residual risk after mitigation, maneuver cost, operational impact.

### 3. Share / Transfer  
- **Goal:** Spread risk via cooperative mechanisms.  
- **Considerations:** Liability agreements, insurance coverage, joint operations.  
- **Parameters:** Insurance premium, shared risk percentage, expected payout in case of collision.

### 4. Accept  
- **Goal:** Acknowledge risk but take no preventive action.  
- **Considerations:** Low probability, minor potential impact, mission priority.  
- **Parameters:** Expected cost of collision, risk tolerance, cost of maneuvers.

### 5. Do Nothing  
- **Goal:** Default when risk is negligible.  
- **Considerations:** Cost exceeds expected benefit, extremely low probability.  
- **Parameters:** Risk probability, potential loss, operational cost of maneuver.

---

## Moving Toward Smarter Decisions  

To overcome the dilemma and optimize strategies:  
- **Coordination protocols:** Shared decision frameworks or AI arbitration to assign responsibility fairly.  
- **Insurance & contracts:** Risk can be shared or transferred to incentivize safe behavior.  
- **AI-enhanced decision support:** Integrates technical risk, cost models, and game theory payoffs to suggest optimal strategies.  

✅ This layer allows the **Tomorrow pipeline** to not only predict risks but also **quantify costs, incentives, and optimal strategies**, making autonomous or assisted maneuvers rational, fair, and efficient.

```mermaid

flowchart LR
  %% === FUTURE PIPELINE ===
  subgraph FUTURE["Tomorrow with AI/ML + Game Theory"]
    direction TB
    A2[Ground-based Observations: Radar, Optical, GNSS] -->|Raw Tracking Data| B2[Orbit Determination]
    A3[Space-based Observations: Crosslinks, Onboard Sensors] -->|Supplementary Measurements| J2[Data Fusion Layer Multi-source Sensor Fusion]
    B2 -->|State Vector| C2[TLE Generation - for SGP4]
    B2 -->|State Vector| D2[Ephemeris Generation - OEM SPICE]

    C2 -->|Catalogs| J2
    D2 -->|Catalogs| J2

    J2 -->|Unified State + Covariance| E2[Propagation and Prediction Models]
    E2 -->|Trajectories + Uncertainty| K2[Risk Inference Engine ML and Probabilistic Forecasting]

    K2 -->|Risk Assessment + Ranked Options| L2[Decision Support Layer Optimization and Game Theory]

    %% Embed payoff logic inside decision support
    subgraph Payoff["Game Theory Payoff Matrix"]
      direction TB
      P1[Maneuver vs Not Maneuver]
      P2["(-1,-1) Both Maneuver"]
      P3["(-1,0) A Maneuvers, B Free Rides"]
      P4["(0,-1) A Free Rides, B Maneuvers"]
      P5["(-100,-100) Neither Maneuvers"]
      P1 --> P2 & P3 & P4 & P5
    end
    L2 --> Payoff

    L2 -->|Candidate Maneuver Strategy| M2[Autonomous Maneuver Execution]
    M2 -->|Executed Maneuver Data| N2[Post-Maneuver Feedback Loop]
    N2 -->|Updated State + CDM Outcomes| O2[Continuous Learning Federated RL Supervised ML]
    O2 --> J2

    K2 -.->|ML Opportunities: Supervised, Bayesian Updates, Reinforcement Learning, Graph NN| L2
  end

  %% === Styling ===
  class J2,K2,L2,M2,N2,O2 new;
  classDef new fill:#ffe599,stroke:#cc9900;

```
