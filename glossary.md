# Glossary of Terms

This glossary provides concise definitions of the most important concepts used throughout this project. Readers who are new to quantum computing may find this section useful as a quick reference while reading the blog.

---

## Qubit

A qubit, or quantum bit, is the fundamental unit of information in a quantum computer. Unlike a classical bit, which can only be either 0 or 1, a qubit can exist in a superposition of both states simultaneously.

---

## Superposition

Superposition is a quantum phenomenon that allows a qubit to exist in a combination of multiple states at the same time. It is one of the key properties that distinguishes quantum computing from classical computing.

---

## Entanglement

Entanglement is a quantum correlation between two or more qubits. When qubits are entangled, the state of one qubit becomes related to the state of the others, even when they are physically separated.

---

## Quantum Gate

A quantum gate is an operation that modifies the state of one or more qubits. Quantum gates are the building blocks of quantum circuits and play a role similar to logic gates in classical computing.

---

## Quantum Circuit

A quantum circuit is a sequence of quantum gates applied to qubits in order to perform a computation. Quantum algorithms are typically represented as quantum circuits.

---

## Noise

Noise refers to unwanted disturbances that alter the state of a quantum system during computation. Noise is one of the primary challenges in modern quantum computing.

---

## Decoherence

Decoherence is the process by which a quantum system loses its quantum properties due to interactions with its environment. It is one of the major sources of quantum noise.

---

## NISQ

NISQ stands for Noisy Intermediate-Scale Quantum. The term describes the current generation of quantum computers, which contain a moderate number of qubits but are still affected by significant noise.

---

## Quantum Error Correction (QEC)

Quantum Error Correction is a collection of techniques designed to protect quantum information by encoding logical qubits into multiple physical qubits. It is considered the long-term solution to quantum noise.

---

## Quantum Error Mitigation (QEM)

Quantum Error Mitigation refers to techniques that reduce the impact of noise without requiring full Quantum Error Correction. These methods are particularly useful for NISQ devices.

---

## Zero-Noise Extrapolation (ZNE)

Zero-Noise Extrapolation is a Quantum Error Mitigation technique that estimates the result of a noise-free quantum computation by analyzing measurements obtained under different noise levels.

---

## Noise Scaling

Noise Scaling is the process of artificially increasing the effective noise experienced by a quantum circuit while preserving its logical behavior. It is a key component of Zero-Noise Extrapolation.

---

## Circuit Folding

Circuit Folding is a Noise Scaling technique in which quantum gates are replaced by equivalent gate sequences that increase the number of operations executed, thereby amplifying noise without changing the intended computation.

---

## Richardson Extrapolation

Richardson Extrapolation is a mathematical technique used to estimate the value of a function at a point that cannot be measured directly. In Zero-Noise Extrapolation, it is used to estimate the zero-noise expectation value.

---

## Observable

An observable is a measurable physical quantity in a quantum system. Examples include Pauli operators and combinations such as Z ⊗ Z.

---

## Expectation Value

The expectation value represents the average outcome of measuring an observable over many repetitions of the same quantum experiment.

---

## Fidelity

Fidelity is a measure of similarity between two quantum states. A fidelity value of 1 indicates identical states, while lower values indicate increasing differences.

---

## Density Matrix

A density matrix is a mathematical representation of a quantum state that can describe both pure states and mixed states. Density matrices are commonly used when modeling noisy quantum systems.

---

## Depolarizing Noise

Depolarizing Noise is a noise model in which a quantum state experiences random Pauli errors, gradually driving it toward a completely mixed state.

---

## Bit-Flip Noise

Bit-Flip Noise is a noise model that randomly changes the state of a qubit from |0⟩ to |1⟩ or vice versa. It is represented by the Pauli-X operator.

---

## Phase-Flip Noise

Phase-Flip Noise is a noise model that changes the phase of a quantum state without directly altering its computational basis value. It is represented by the Pauli-Z operator.
