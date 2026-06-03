# Quantum Noise Models

In the previous sections, we learned that quantum computers are highly sensitive to noise. Even when a quantum algorithm is mathematically correct, imperfections in the hardware can alter the quantum state and produce inaccurate results.

To study the effectiveness of Quantum Error Mitigation techniques, researchers often use mathematical models that describe different types of noise. These models help us understand how errors affect quantum computations and provide controlled environments for testing mitigation strategies.

In this project, three commonly used noise models were investigated:

* Depolarizing Noise
* Bit-Flip Noise
* Phase-Flip Noise

Although all three models introduce errors into the quantum computation, they affect quantum states in fundamentally different ways. Understanding these differences is important because the performance of Zero-Noise Extrapolation may vary depending on the underlying noise mechanism.

## Depolarizing Noise

Depolarizing Noise is one of the most widely used noise models in quantum computing research. It is often considered a general-purpose model because it captures the effect of random errors without assuming a specific physical source.

The intuition behind Depolarizing Noise is simple. Imagine that a quantum gate is executed on a qubit. In an ideal quantum computer, the gate would perform the desired operation perfectly. In a noisy device, however, there is always a small probability that something unexpected happens during execution.

Instead of applying the intended operation exactly, the qubit may experience a random disturbance. This disturbance can behave like a Pauli-X error, a Pauli-Y error, or a Pauli-Z error. Since these possibilities are treated symmetrically, the resulting quantum state gradually loses information about its original direction.

From a geometric perspective, Depolarizing Noise pushes the quantum state toward a completely mixed state. As the noise level increases, the quantum system becomes less distinguishable from a random state.

Because of its simplicity and generality, Depolarizing Noise is frequently used as a benchmark when evaluating Quantum Error Mitigation techniques. In this project, it serves as one of the primary test cases for assessing the effectiveness of Zero-Noise Extrapolation.

The Depolarizing channel is defined as:

$$
\rho' =
(1-p)\rho
+
\frac{p}{3}
(X\rho X + Y\rho Y + Z\rho Z)
$$
### Characteristics

- Randomized quantum errors
- Affects both amplitudes and phases
- Frequently used in simulation studies

---

## Bit-Flip Noise

To understand Bit-Flip Noise, it is useful to begin with a familiar example from classical computing.

Suppose a classical bit stores the value 0. Due to a hardware malfunction or transmission error, the stored value may accidentally change to 1. Similarly, a bit that should be 1 may become 0. This type of error is known as a bit flip.

Quantum systems can experience a very similar phenomenon.

In a quantum computer, a qubit may unintentionally change its state during computation. A qubit that should remain in the state |0⟩ may be transformed into |1⟩, while a qubit that should be in |1⟩ may become |0⟩. This behavior is described by the Bit-Flip Noise model.

Mathematically, Bit-Flip Noise is represented using the Pauli-X operator, which acts as the quantum equivalent of the classical NOT gate. Whenever a bit-flip error occurs, the quantum state is effectively acted upon by an unwanted X gate.

Although the concept appears simple, the consequences can be significant. A single bit-flip error may propagate through a quantum circuit and alter the final measurement outcome. In circuits containing entangled qubits, the effect can become even more pronounced because the error may influence the correlations between multiple qubits.

Bit-Flip Noise is particularly useful as a benchmark because it provides an intuitive and easily interpretable model of quantum errors. In this project, it allows us to investigate how effectively Zero-Noise Extrapolation can recover accurate expectation values when qubits experience unwanted state inversions.

The Bit-Flip channel is described by:

$$
\rho' = (1-p)\rho + pX\rho X
$$

### Characteristics

- Changes the computational basis state
- Similar to classical bit inversion
- Easy to visualize and analyze

---

## Phase-Flip Noise

Unlike Bit-Flip Noise, Phase-Flip Noise does not directly change the measured value of a qubit. This makes it one of the more subtle forms of quantum noise.

To understand why, recall that a quantum state contains not only probabilities but also phase information. Quantum algorithms often rely on these phases to create constructive and destructive interference patterns that guide the computation toward the correct answer.

A Phase-Flip error alters this phase information without necessarily changing the measurement outcome in the computational basis.

For example, consider a qubit prepared in a superposition state. A phase-flip error may modify the relative phase between the components of the superposition while leaving the probabilities unchanged. As a result, the qubit may still appear normal when measured directly, even though its quantum information has been corrupted.

This behavior has no true classical equivalent. In classical computing, changing a value usually means changing the stored bit itself. In quantum computing, however, changing the phase of a state can dramatically affect the outcome of future quantum operations.

Phase-Flip Noise is commonly modeled using the Pauli-Z operator. When a phase-flip error occurs, the quantum state experiences an unwanted Z operation that changes the sign of specific components of the state vector.

Because many quantum algorithms depend heavily on interference effects, phase errors can be particularly damaging. For this reason, studying Phase-Flip Noise provides valuable insight into the robustness of Quantum Error Mitigation techniques.

The Phase-Flip channel is described by:

$$
\rho' = (1-p)\rho + pZ\rho Z
$$

In this project, Phase-Flip Noise serves as an important test case for evaluating how well First-Order and Second-Order Richardson Extrapolation can recover the ideal expectation value from noisy measurements.



### Characteristics

- Preserves measurement probabilities
- Alters phase relationships
- Can significantly affect interference effects

---

# Comparison of Noise Models

| Noise Model | Pauli Operator | Effect |
|-------------|---------------|---------|
| Depolarizing | X, Y, Z | Randomizes the quantum state |
| Bit-Flip | X | Flips |0⟩ and |1⟩ |
| Phase-Flip | Z | Changes the phase of the state |

---
## Why Study Multiple Noise Models?

Real quantum hardware is affected by many different sources of noise simultaneously. Some errors may behave like bit flips, others may alter quantum phases, and some may introduce more general random disturbances.

Because of this complexity, evaluating an error mitigation technique using only a single noise model may provide an incomplete picture of its performance.

For this reason, this project investigates Zero-Noise Extrapolation under three different noise models: Depolarizing Noise, Bit-Flip Noise, and Phase-Flip Noise. By comparing the mitigation performance across these scenarios, it becomes possible to better understand the strengths and limitations of Richardson Extrapolation under different error mechanisms.

The next section describes the experimental setup used to implement these noise models and evaluate the effectiveness of Zero-Noise Extrapolation.


