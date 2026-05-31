# Experimental Setup

## Overview

To evaluate the effectiveness of Zero-Noise Extrapolation (ZNE), a series of experiments were conducted using Qiskit and Qiskit Aer simulators.

The experiments focused on measuring how different quantum noise models affect circuit performance and how Richardson Extrapolation can mitigate these errors.

---

# Software Environment

The implementation was developed using:

- Python
- Qiskit
- Qiskit Aer
- NumPy
- Matplotlib

Qiskit Aer was used to simulate noisy quantum circuits and generate density matrices for evaluating expectation values and state fidelity.

---

# Quantum Circuit

A two-qubit variational quantum circuit was designed for the experiments.

The circuit contains:

- RY rotation gates
- RX rotation gates
- CNOT gates

The chosen circuit includes both single-qubit operations and entangling operations, making it suitable for studying the effect of noise accumulation.



The circuit structure is illustrated below:

```python
qc.ry(theta[0], 0)
qc.ry(theta[2], 1)

qc.rx(theta[1], 0)

qc.cx(0,1)

qc.ry(theta[3], 0)
qc.ry(theta[4], 1)

qc.cx(0,1)

qc.rx(theta[5], 0)
```

## Variational Quantum Circuit

The following variational quantum circuit was used throughout the experiments.

![Variational Circuit](images/1.png)

Figure 1: The variational quantum circuit used in the experiments.
---

# Noise Models

Three different noise models were investigated:

## 1. Depolarizing Noise

Depolarizing errors were applied to:

- RX gates
- RY gates
- CNOT gates

Both one-qubit and two-qubit depolarizing channels were considered.

---

## 2. Bit-Flip Noise

Bit-flip errors were simulated using Pauli-X channels.

The noise model randomly flips qubit states with probability p.

---

## 3. Phase-Flip Noise

Phase-flip errors were simulated using Pauli-Z channels.

This model modifies the phase of the quantum state without changing the computational basis measurement outcome.

---

# Noise Strength

The experiments were performed using multiple noise probabilities.

Typical values included:

- p = 0.001
- p = 0.005
- p = 0.01
- p = 0.02

Additional experiments were conducted at larger noise levels to evaluate the behavior of the extrapolation process.

---

# Fidelity Evaluation

To quantify the impact of noise, the fidelity between the ideal state and the noisy state was computed.

State fidelity measures the similarity between two quantum states.

A fidelity value of:

F = 1

indicates identical states.

Lower fidelity values indicate stronger noise effects.

---

# Expectation Value Measurement

The observable used in this project was:

⟨Z ⊗ Z⟩

which measures the correlation between the two qubits.

Expectation values were computed from the density matrix obtained from noisy simulations.

---

# Noise Scaling Factors

To perform Zero-Noise Extrapolation, the following scale factors were used:

- s = 1
- s = 3
- s = 5

The original circuit corresponds to:

s = 1

while larger scale factors were generated using circuit folding.

---

# Circuit Folding Strategy

Noise amplification was achieved through global circuit folding.

For each gate G:

G → GG†G

This operation preserves the logical functionality of the circuit while increasing its effective noise level.

Higher scaling factors introduce additional folded gate sequences and therefore accumulate more noise.

---

# Richardson Extrapolation

Two extrapolation strategies were evaluated:

## First-Order Richardson Extrapolation

Uses measurements obtained from:

- s = 1
- s = 3

to estimate the zero-noise expectation value.

---

## Second-Order Richardson Extrapolation

Uses measurements obtained from:

- s = 1
- s = 3
- s = 5

to remove additional error terms and improve estimation accuracy.

The performance of both approaches was compared across all investigated noise models.
