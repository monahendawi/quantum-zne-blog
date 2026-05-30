# Related Work

## Early Efforts in Quantum Error Mitigation

As quantum computers entered the Noisy Intermediate-Scale Quantum (NISQ) era, researchers quickly recognized that quantum noise would become one of the primary obstacles to reliable computation. While Quantum Error Correction provides a theoretically robust solution, its large qubit overhead makes it impractical for current hardware.

This challenge motivated the development of Quantum Error Mitigation (QEM) techniques, which aim to improve computational accuracy without requiring fault-tolerant quantum devices.

---

## Zero-Noise Extrapolation

One of the most influential contributions in this area was introduced by Temme, Bravyi, and Gambetta in 2017. Their work proposed **Zero-Noise Extrapolation (ZNE)** as a practical method for mitigating errors in short-depth quantum circuits.

The central idea is to intentionally increase the noise level of a quantum circuit and then extrapolate the measured expectation values back to the ideal zero-noise limit.

This approach demonstrated that meaningful error reduction could be achieved without introducing additional logical qubits.

---

## Noise Scaling Through Circuit Folding

A key challenge in Zero-Noise Extrapolation is controlling the effective noise level.

To address this issue, researchers introduced **circuit folding**, where a gate is replaced by an equivalent sequence:

G → GG†G

Although the logical operation remains unchanged, the circuit becomes deeper and accumulates more noise.

This technique enables controlled noise amplification while preserving the intended quantum computation.

Circuit folding has become one of the most widely used approaches for implementing ZNE on both simulators and real quantum hardware.

---

## Richardson Extrapolation

Several extrapolation methods have been proposed for estimating the zero-noise expectation value.

Among these methods, **Richardson Extrapolation** is one of the most popular due to its simplicity and effectiveness.

The first-order Richardson method removes the dominant noise contribution by combining measurements obtained at different noise scales.

Researchers later extended this idea to higher-order Richardson extrapolation, which can eliminate additional error terms and improve estimation accuracy.

However, higher-order methods may also become more sensitive to statistical fluctuations and imperfect noise scaling.

---

## Noise Models in Previous Studies

Many ZNE studies primarily focus on depolarizing noise because it provides a simple and mathematically convenient model for quantum errors.

However, real quantum systems often exhibit more structured error mechanisms such as:

- Bit-Flip Noise
- Phase-Flip Noise
- Amplitude Damping
- Readout Errors

The effectiveness of ZNE may vary significantly depending on the underlying noise process.

---

## Research Gap

Most existing studies focus on demonstrating the effectiveness of Zero-Noise Extrapolation under a single noise model or using standard first-order Richardson extrapolation.

Fewer works provide a direct comparison between:

- Multiple quantum noise models
- First-order Richardson extrapolation
- Second-order Richardson extrapolation

This project addresses this gap by evaluating Zero-Noise Extrapolation under depolarizing, bit-flip, and phase-flip noise while comparing the performance of first-order and second-order Richardson extrapolation techniques.
