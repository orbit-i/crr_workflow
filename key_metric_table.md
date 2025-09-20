### Key Metrics and Parameters for Conjunction Risk Assessment and Response Workflow

| Category               | Parameters / Key Metrics                                       | Possible Sources / Defined From         |
|------------------------|---------------------------------------------------------------|-----------------------------------------|
| **1. Data Fusion Processing** | Orbital state vectors                                  | Ground tracking, onboard sensors, TLE   |
|                        | Ephemeris data                                                | State vectors                   |
|                        | TLE data                                                      | Public catalogs                          |
|                        | Measurement uncertainties                                     | Tracking system error models             |
|                        | Environmental data (space weather, drag, radiation)           | Space weather centers, atmospheric models|
| **2. Risk Inference Engine** | Event geometry (miss distance, TCA, rel velocity)       | Conjunction event                        |
|                        | Probability of collision (Pc) and Covariance                  | Risk metrix|
|                        | Covariance matrix                                             | Risk metrix|
|                        | Uncertainty Growth Rate                                       | Risk metrix|
|                        | Risk thresholds                                               | Operator-defined criteria               |
|                        | CDM (Conjunction Data Message)                                | Standardized CCSDS                       |
| **3. Decision Support** | Strategy categories (no action, monitor, maneuver)           | Operator policies, best practices       |
|                        | Payout or cost estimation (fuel, downtime, insurance, loss)   | Insurance models, mission cost models   |
|                        | Cost-benefit trade-offs                                       | Decision analysis framework             |
|                        | Satellite Constraint                                          | Operators Provision   |
|                        | Historical Maneuver Behaviour                                 | Historical TLE Data   |
| **4. Execution**       | Maneuver execution (delta-v, trajectory update)               | Spacecraft attitude and orbit control system |
|                        | Autonomous or manual decision                                 | Onboard autonomy, ground control        |
|                        | Post-conjunction feedback                                     | Telemetry, performance evaluation       |
