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

Voltage and frequency are coupled to performance and power. Frequency determines how many operations the circuit can perform per second, higher frequence = higher performance. 

But, higher frequency also means higher supply voltage to meet timing constraints. 

Lowering voltage has a higher impact because in the *Dynamic power equation* voltage appears squared.

3. What is DVFS, and how would you use it to optimize power in a GPU?

DVFS stands for Dynamic Voltage and Frequency Scaling is a technique that adjust GPU's voltage and frequency based on workload demand.

DVFS lowers voltage and frquency during light workloads and increases them when higher perfomance is needed, creating optimum performance.

4. Why are GPUs particularly more power-hungry than CPUs?

GPUs are designed for high  throughput using massive parallelism.

5. What parts of a GPU pipeline consume the most power during graphics workloads versus compute workloads?

----

6. What is activity factor (α), and how does it relate to dynamic power?

The activity factor, represents how frequently a signal toggles between 0 and 1. It affects the dynamic power, because the higher switching activity increases amount of capacitance being charged and discharged, which affects dynamic power. 

7. How do SIMD/SIMT execution models affect power efficiency in GPUs?

SIMD (Single Instruction Multiple Data) and SIMT (Single Instruction Multiple Threads) both implement parallelism, which improves power efficiency because more work is done per instruction fetch and per clock cycle, reducing control overhead and wasted energy. 
