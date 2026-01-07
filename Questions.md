1. What is the difference between dynamic power and leakage power? How can each be reduced in a modern GPU?

Dynamic power is the power consumed when transistors switch states, mainly to charge and discharge or capacitances. This is also proportional to the dynamic power equation. In *GPU* dynamic power is high due to massive parallel switching across compute units. 

Dynamic power can be reduced by techniques such as: 
- clock gating
- reducing switching activity
- DVFS
- optimizing workloads to improve data locality. 

Leakage power, also called as static opwer, is the power consumed when the circuit is idle. Due to subthreshold leakage and gate leakage in transistors. The smaller the node, leakage becomes more significant. 

Leakage power can be reduced using: 
- power gating
- high-vt cells (higher voltage is required to switch ON, which leaks less current)
- multi-Vt Design (use LVT only where needed, HVT anywhere else )
    - Using HVT everywhere would increase delay.

2. Explain the relationship between voltage, frequency, performance, and power. Why does lowering voltage have a stronger impact on power than lowering frequency?