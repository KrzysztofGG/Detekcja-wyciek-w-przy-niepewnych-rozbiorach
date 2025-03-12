# Detekcja-wycieków-przy-niepewnych-rozbiorach

#### Model-based leakage diagnosis
- larger number of pressure sensors than flow sensors
- MOST IMPORTANT: Find difference between measurements and model estimates - this indicates leakage
- Consumer demand is greatest source of uncertainty
- WDS can be reduced to iteratively examining the feasibility of a Linear Program

#### Leakage detection by interval-model invalidation
- Uncertainties required in the model are derived from historical data
- Fault free model is given by a linear problem
- nodes are grouped based on the amount  of sensors in the system


**Leakage detection consist of 5 steps**
1. Initial bounds:
chosen based on physical system specification
head vectors: h_ = [h_l(m), h_h(m)]
flow state: q_ = [q_l(m), q_h(m)] derived from: f(𝒒(𝑘)) + 𝐵𝒉(𝑘) = 0
2. Bounding linearization
Enclose uncertainty function (water intake) within some bounds
make nonlinear uncertainty function into linear by adding auxiliary (pomocnicze) parameters
3. Form problem for relaxation
rewrite the problem using lower and upper bounds as seperate equations
formulate two linear problems LPmin and LPmax to get the bounds of state variable xi (state of the whole system x=[ qT hT]T)
4. Model validation
count 2(nl + nn) LPs to find state of the whole system (all state variables xi), if at least on problem is not feasible then we have a fault in the system
5. Iterative model validation
Counter x is used to tigten the bounds of uncertainty function in each iteration as long as bounds are changing noticeably

#### Leakage localization using an interval-model
New linear problem definition
1. Initial bounds
Based on leake magnitudes
2. Bounding linearization
Again add parameters to enclose uncertainty function in linear problem (head-loss and leakege functions for each node in system)
3. Formulation of the relaxed problem and calculation of leakage bounds
formulate constaints for linear problem, assume only one leakage in the system
Solve LPmin and LPmax nl + nn number of times to find state bounds [xl, xu]
Solve LPmin2L and LPmax2L for each node to found leakege size boudns [q_leak_l, q_leak_u] if problem infeasible: q_leak = [0, 0]
4. Iterative reduction of leakage bounds
get the state of the system and use it to tighten coefficent bounds, run untill they stop changing much
5. Considering multiple time-steps to improve localization
if leakage persists for multiple time steps (which is exptected) we can use final bounds from previous timestamp as initial bounds for new run

#### Localization priority index
Determine all possible leak locations as nodes with nonzero upper bound *c* (leak emitter coefficient) - highest upper bound has higherst priority
