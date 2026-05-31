# Results and Discussion

## Overview

This section presents the experimental results obtained from applying Zero-Noise Extrapolation (ZNE) to a variational quantum circuit under different quantum noise models.

The effectiveness of both First-Order and Second-Order Richardson Extrapolation is evaluated and compared.

---

# Fidelity Analysis

Before applying error mitigation, the impact of each noise model was evaluated using state fidelity.

The following results were obtained for a noise probability of p = 0.01:

| Noise Model | Fidelity |
|------------|-----------|
| Depolarizing Noise | 0.9528 |
| Bit-Flip Noise | 0.9254 |
| Phase-Flip Noise | 0.9303 |

These results indicate that all investigated noise channels degrade the quantum state, with bit-flip noise producing the largest reduction in fidelity.

---

# Depolarizing Noise Results

For depolarizing noise, Zero-Noise Extrapolation produced the strongest improvement among all investigated noise models.

| Method | Error |
|----------|----------|
| No ZNE | 0.03547 |
| First-Order Richardson | 0.00305 |
| Second-Order Richardson | 0.00031 |

Second-Order Richardson Extrapolation reduced the estimation error by approximately 115× compared to the original noisy result.


![ZNE vs Noise](images/4.png)

Figure 4: Comparison between the noisy expectation value and the mitigated expectation value obtained using Zero-Noise Extrapolation.

---

# Bit-Flip Noise Results

For bit-flip noise, both first-order and second-order Richardson extrapolation improved the results.

| Method | Error |
|----------|----------|
| No ZNE | 0.05764 |
| First-Order Richardson | 0.01247 |
| Second-Order Richardson | 0.00655 |

The second-order approach reduced the error by approximately nine times compared to the original noisy result.

---

# Phase-Flip Noise Results

Phase-flip noise showed the largest benefit from higher-order extrapolation.

| Method | Error |
|----------|----------|
| No ZNE | 0.04570 |
| First-Order Richardson | 0.00541 |
| Second-Order Richardson | 0.00085 |

The error reduction achieved by second-order Richardson extrapolation was significantly greater than that obtained using the first-order method.

---


# First-Order vs Second-Order Richardson Extrapolation

The mitigation performance of First-Order and Second-Order Richardson Extrapolation was evaluated for all investigated noise models.

| Noise Model | No ZNE Error | First-Order Richardson | Second-Order Richardson |
|------------|------------|------------|------------|
| Depolarizing | 0.03547 | 0.00305 | 0.00031 |
| Bit Flip | 0.05764 | 0.01247 | 0.00655 |
| Phase Flip | 0.04570 | 0.00541 | 0.00085 |

The results show that both extrapolation methods significantly reduce the estimation error compared to the original noisy measurements. However, Second-Order Richardson Extrapolation consistently achieves the lowest error across all investigated noise models.
![Error Reduction](images/5.png)

Figure 5: Error reduction achieved by Zero-Noise Extrapolation across different noise models.


---

# Improvement Analysis

To better quantify the effectiveness of error mitigation, the improvement factor achieved by Second-Order Richardson Extrapolation was calculated.
The improvement factor is defined as

```text
Improvement Factor = Error Before ZNE / Error After ZNE
```
| Noise Model | Improvement Factor |
|------------|------------|
| Depolarizing | 115× |
| Bit Flip | 8.8× |
| Phase Flip | 53.6× |

The improvement factor was computed as:

Improvement Factor = Error Before ZNE / Error After Second-Order ZNE

---

# Discussion

Several important observations can be drawn from the experiments:

### Observation 1

Quantum noise significantly affects the accuracy of quantum computations even for relatively small circuits.

### Observation 2

Zero-Noise Extrapolation successfully reduced the estimation error under all investigated noise models.

### Observation 3

Second-Order Richardson Extrapolation consistently outperformed First-Order Richardson Extrapolation.

### Observation 4

The largest improvement was observed for depolarizing noise, where the estimation error decreased from 0.03547 to 0.00031 after applying Second-Order Richardson Extrapolation.

### Observation 5

Phase-flip noise also benefited substantially from higher-order extrapolation, achieving an improvement factor of approximately 53.6×.

### Observation 6

Bit-flip noise showed the smallest relative improvement among the investigated noise models, although significant error reduction was still achieved.

---

# Key Findings

The experiments demonstrate that:

- Zero-Noise Extrapolation is an effective Quantum Error Mitigation technique.
- Circuit folding successfully amplifies noise while preserving circuit functionality.
- Richardson Extrapolation recovers expectation values closer to the ideal result.
- Second-Order Richardson Extrapolation consistently outperforms First-Order Richardson Extrapolation.
- The best mitigation performance was achieved under depolarizing noise.
- An improvement factor of approximately 115× was obtained for depolarizing noise using Second-Order Richardson Extrapolation.


