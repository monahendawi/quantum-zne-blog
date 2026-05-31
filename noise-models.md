# Quantum Noise Models

## Why Do We Need Noise Models?

Quantum computers operate in highly sensitive environments. Even small disturbances can alter the state of a qubit and affect the outcome of a quantum computation.

To study and evaluate error mitigation techniques such as Zero-Noise Extrapolation (ZNE), researchers often use mathematical noise models that simulate different types of quantum errors.

In this project, three common quantum noise models were investigated:

- Depolarizing Noise
- Bit-Flip Noise
- Phase-Flip Noise

---

# Depolarizing Noise

Depolarizing noise is one of the most widely used noise models in quantum computing.

It represents a random error process in which a qubit loses information about its original state and becomes partially randomized.

With probability p, the qubit undergoes a random Pauli operation:

X, Y, or Z

while with probability (1-p), the qubit remains unchanged.

Because of its simplicity, depolarizing noise is commonly used as a benchmark for evaluating quantum algorithms and error mitigation techniques.
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

# Bit-Flip Noise

Bit-flip noise is analogous to classical bit errors.

Under this noise model, a qubit may change from:

|0⟩ → |1⟩

or

|1⟩ → |0⟩

This error is represented by the Pauli-X operator.

The bit-flip channel applies an X gate with probability p.
The Bit-Flip channel is described by:

$$
\rho' = (1-p)\rho + pX\rho X
$$

### Characteristics

- Changes the computational basis state
- Similar to classical bit inversion
- Easy to visualize and analyze

---

# Phase-Flip Noise

Unlike bit-flip noise, phase-flip noise does not change the measured value of the qubit.

Instead, it modifies the relative phase of the quantum state.

This error is represented by the Pauli-Z operator.

For example:

|+⟩ → |−⟩

even though the probabilities of measuring 0 or 1 may remain unchanged.

Phase-flip errors are particularly important because many quantum algorithms rely heavily on phase information.
The Phase-Flip channel is described by:

$$
\rho' = (1-p)\rho + pZ\rho Z
$$

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

# Noise Models Used in This Project

To evaluate the effectiveness of Zero-Noise Extrapolation, the three noise models above were implemented using Qiskit Aer noise channels.

The performance of ZNE was then analyzed under each noise model and compared using both First-Order and Second-Order Richardson Extrapolation.
