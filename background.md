# Background

## The Challenge of Quantum Noise

Quantum computing has the potential to revolutionize many fields, including optimization, cryptography, drug discovery, and machine learning. Unlike classical computers, which process information using bits, quantum computers use **qubits** that can exist in superposition states and become entangled with one another.

A general single-qubit quantum state can be represented as:

$$
|\psi\rangle = \alpha |0\rangle + \beta |1\rangle
$$

where

$$
|\alpha|^2 + |\beta|^2 = 1
$$

to satisfy the normalization condition.

These unique properties enable quantum computers to perform certain computations more efficiently than classical systems. However, today's quantum devices face a major challenge: **noise**.

Quantum systems are extremely sensitive to their environment. Even small interactions with surrounding particles can disturb quantum states and introduce errors during computation. As a result, the output of a quantum circuit may differ significantly from the ideal result.

---

## NISQ Devices

Current quantum computers belong to the **Noisy Intermediate-Scale Quantum (NISQ)** era.

NISQ devices typically contain tens to hundreds of qubits, but they are not yet capable of performing fault-tolerant quantum computation. Noise accumulates throughout circuit execution, limiting the depth and complexity of algorithms that can be executed reliably.

Common sources of quantum noise include:

- Decoherence
- Gate imperfections
- Environmental interactions
- Measurement errors

These errors reduce the fidelity of quantum states and negatively affect computational accuracy.

---

## Quantum Error Correction vs Quantum Error Mitigation

To address quantum noise, researchers have developed two main approaches:

### Quantum Error Correction (QEC)

Quantum Error Correction protects quantum information by encoding a logical qubit into multiple physical qubits. While QEC provides a long-term solution for fault-tolerant quantum computing, it requires substantial hardware resources that are currently unavailable in most NISQ devices.

### Quantum Error Mitigation (QEM)

Quantum Error Mitigation aims to reduce the impact of noise without requiring additional logical qubits. Instead of correcting errors directly, mitigation techniques estimate what the ideal noise-free result would have been.

As a result, QEM has become an attractive solution for near-term quantum computers.

---

## Zero-Noise Extrapolation

One of the most widely used Quantum Error Mitigation techniques is **Zero-Noise Extrapolation (ZNE)**.

The main idea behind ZNE is simple:

1. Execute a quantum circuit under different effective noise levels.
2. Measure the corresponding expectation values.
3. Extrapolate these measurements back to the zero-noise limit.

Rather than eliminating noise physically, ZNE estimates the result that would have been obtained if no noise were present.

This makes ZNE particularly suitable for current NISQ quantum devices.

---

## Motivation of This Project

This project investigates the effectiveness of Zero-Noise Extrapolation under multiple quantum noise models, including:

- Depolarizing Noise
- Bit-Flip Noise
- Phase-Flip Noise

In addition, the project compares the performance of **First-Order Richardson Extrapolation** and **Second-Order Richardson Extrapolation** to evaluate the benefits of higher-order error mitigation techniques.
