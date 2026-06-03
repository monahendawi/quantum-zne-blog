# Results and Discussion

## Overview

After developing the theoretical foundations of Zero-Noise Extrapolation and implementing the mitigation framework in Qiskit, the next step is to evaluate its practical performance.

The objective of these experiments is not simply to produce numerical results, but to understand how different types of quantum noise affect a computation and how effectively Zero-Noise Extrapolation can recover the ideal outcome.

Three noise models were investigated throughout this study: Depolarizing Noise, Bit-Flip Noise, and Phase-Flip Noise. For each model, the performance of First-Order and Second-Order Richardson Extrapolation was evaluated and compared.

The results presented in this section provide insight into both the strengths and limitations of Zero-Noise Extrapolation when applied to realistic noisy quantum circuits.

---

# Fidelity Analysis

The fidelity results provide an initial indication of how strongly each noise model disturbs the quantum state before any mitigation technique is applied.

Among the investigated noise models, Bit-Flip Noise produced the lowest fidelity value, indicating the strongest deviation from the ideal quantum state. This suggests that unwanted state inversions can significantly alter the computation even before the final measurement stage.

Depolarizing Noise produced the highest fidelity among the three models. Although it introduces random disturbances, its overall effect on the quantum state was less severe for the circuit considered in this study.

These observations establish a useful baseline for evaluating the effectiveness of Zero-Noise Extrapolation in the following experiments.


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

The results obtained under Depolarizing Noise demonstrate the effectiveness of Zero-Noise Extrapolation as an error mitigation strategy.

Without mitigation, the measured expectation value deviated noticeably from the ideal result. Applying First-Order Richardson Extrapolation significantly reduced the error, while Second-Order Richardson Extrapolation produced an even larger improvement.

The reduction from 0.03547 to 0.00031 corresponds to an improvement factor of approximately 115×. This represents the strongest mitigation performance observed in the entire study.

One possible explanation is that the smooth behavior of Depolarizing Noise aligns particularly well with the assumptions underlying Richardson Extrapolation, allowing the extrapolation procedure to estimate the zero-noise limit with high accuracy.

---

# Bit-Flip Noise Results

For bit-flip noise, both first-order and second-order Richardson extrapolation improved the results.

| Method | Error |
|----------|----------|
| No ZNE | 0.05764 |
| First-Order Richardson | 0.01247 |
| Second-Order Richardson | 0.00655 |

The second-order approach reduced the error by approximately nine times compared to the original noisy result.
Bit-Flip Noise presented a more challenging scenario for error mitigation.

Although both extrapolation methods successfully reduced the error, the overall improvement was smaller than that observed for Depolarizing Noise.

This behavior suggests that Bit-Flip errors may introduce deviations that are more difficult to model using low-order extrapolation techniques. Nevertheless, the reduction achieved by Second-Order Richardson Extrapolation confirms that Zero-Noise Extrapolation remains beneficial even when the underlying noise mechanism differs significantly from the depolarizing model.

The results demonstrate that higher-order extrapolation continues to provide measurable gains over the simpler First-Order approach.

---

# Phase-Flip Noise Results

Phase-flip noise showed the largest benefit from higher-order extrapolation.

| Method | Error |
|----------|----------|
| No ZNE | 0.04570 |
| First-Order Richardson | 0.00541 |
| Second-Order Richardson | 0.00085 |

The error reduction achieved by second-order Richardson extrapolation was significantly greater than that obtained using the first-order method.
The Phase-Flip experiments revealed a substantial advantage for higher-order extrapolation.

While First-Order Richardson Extrapolation already produced a noticeable improvement, Second-Order Richardson Extrapolation reduced the error by more than an order of magnitude compared to the original noisy result.

This behavior is particularly interesting because Phase-Flip Noise alters phase information rather than directly changing measurement outcomes. Since many quantum computations rely heavily on phase relationships and interference effects, recovering these effects through mitigation can lead to significant improvements in accuracy.

The final error of 0.00085 demonstrates that Zero-Noise Extrapolation remains highly effective even for noise processes that primarily affect quantum phases.

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

| Noise Model | Improvement Factor |
|------------|------------|
| Depolarizing | 115× |
| Bit Flip | 8.8× |
| Phase Flip | 53.6× |

The improvement factor is defined as

```text
Improvement Factor = Error Before ZNE / Error After ZNE
```

---


# Discussion

Several important conclusions can be drawn from the experimental results.

First, all investigated noise models produced noticeable deviations from the ideal quantum computation. This observation highlights the fundamental challenge faced by current NISQ devices and reinforces the need for practical error mitigation techniques.

Second, Zero-Noise Extrapolation consistently improved the quality of the measured expectation values. In every experiment, the mitigated result was closer to the ideal value than the original noisy measurement. This confirms that ZNE successfully captures useful information about how the computation behaves under increasing noise levels.

Third, Second-Order Richardson Extrapolation outperformed First-Order Richardson Extrapolation in all investigated scenarios. By removing additional higher-order error terms, the second-order method was able to provide more accurate estimates of the zero-noise expectation value.

Finally, the mitigation performance varied across different noise models. Depolarizing Noise exhibited the largest improvement factor, while Bit-Flip Noise proved somewhat more challenging to mitigate. These differences suggest that the effectiveness of ZNE depends not only on the magnitude of the noise but also on its underlying structure.

Overall, the results demonstrate that Zero-Noise Extrapolation is a practical and effective error mitigation technique for noisy quantum computations and can substantially improve computational accuracy without requiring additional qubits.

---

# Key Findings

The experiments demonstrate that:

- Zero-Noise Extrapolation is an effective Quantum Error Mitigation technique.
- Circuit folding successfully amplifies noise while preserving circuit functionality.
- Richardson Extrapolation recovers expectation values closer to the ideal result.
- Second-Order Richardson Extrapolation consistently outperforms First-Order Richardson Extrapolation.
- The best mitigation performance was achieved under depolarizing noise.
- An improvement factor of approximately 115× was obtained for depolarizing noise using Second-Order Richardson Extrapolation.


