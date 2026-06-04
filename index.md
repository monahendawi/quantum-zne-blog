# Quantum Error Mitigation using Zero-Noise Extrapolation

## Abstract

Quantum computing has emerged as a promising computational paradigm capable of solving certain problems more efficiently than classical computers. However, current quantum devices operate in the Noisy Intermediate-Scale Quantum (NISQ) era, where noise and hardware imperfections significantly limit computational accuracy. Quantum Error Mitigation (QEM) techniques have therefore become essential for improving the reliability of near-term quantum computations.

This project investigates Zero-Noise Extrapolation (ZNE), one of the most widely used Quantum Error Mitigation techniques. A variational two-qubit quantum circuit was implemented using Qiskit and evaluated under three different noise models: Depolarizing Noise, Bit-Flip Noise, and Phase-Flip Noise. Noise amplification was achieved through Circuit Folding, while First-Order and Second-Order Richardson Extrapolation were used to estimate noise-free expectation values.

Experimental results demonstrate that Zero-Noise Extrapolation significantly reduces estimation errors across all investigated noise models. Furthermore, Second-Order Richardson Extrapolation consistently outperformed First-Order Richardson Extrapolation, achieving the highest mitigation accuracy. The study highlights the effectiveness of ZNE as a practical error mitigation strategy for current NISQ devices and demonstrates its potential for improving the reliability of near-term quantum computations.




# Background

## Why Quantum Computing?

Tech today has reshaped daily living, from smartphones to social media and research. Yet, classical computers struggle with complicated tasks such as modeling molecules, which consume too many resources. For this reason, researchers shifted to quantum computing. This harnesses strange properties like superposition and entanglement to handle these issues. Though we're just starting out, many think it will revolutionize how we deal with major science and engineering challenges.


---

## What is a Qubit?

To understand how quantum computers work, we must first understand the fundamental unit of quantum information: the **qubit**.

In classical computing, information is stored using bits. A bit can only exist in one of two possible states:

* 0
* 1

For example, every image, video, document, or application stored on your computer is ultimately represented as a long sequence of zeros and ones.

A quantum computer uses a different unit of information called a **quantum bit**, or **qubit**.

Unlike a classical bit, a qubit is not restricted to a single state. Instead, it can exist in a combination of multiple states simultaneously. This unique property allows quantum computers to represent information in a much richer way than classical systems.

The difference between classical bits and qubits is summarized below:

| Classical Bit              | Qubit                                                   |
| -------------------------- | ------------------------------------------------------- |
| Can be 0 or 1              | Can be a combination of 0 and 1                         |
| Based on classical physics | Based on quantum mechanics                              |
| Deterministic              | Probabilistic                                           |
| Stores one state at a time | Can represent multiple possibilities before measurement |

Mathematically, a qubit is represented as:

|ψ⟩ = α|0⟩ + β|1⟩

where:

* α and β are complex numbers called probability amplitudes.
* |0⟩ and |1⟩ are the computational basis states.

The probabilities associated with these states must satisfy:

|α|² + |β|² = 1

This condition ensures that the total probability of all possible measurement outcomes equals one.

At first glance, a qubit may seem like a simple extension of a classical bit. However, when multiple qubits interact, they can exhibit uniquely quantum behaviors that have no classical equivalent. These behaviors form the foundation of quantum computing and enable algorithms that would be impossible to implement efficiently on classical machines.


---
Quantum gates are the building blocks of quantum circuits. Instead of classical logic gates that work with bits, these manipulate qubits through unitary operations. When you combine different quantum gates, you can carry out complex calculations.

For this project, the main gates we use are:

**The Pauli-X gate (X)** flips the qubit state, turning ∣0⟩ into ∣1⟩ and the other way around. It's also handy for modeling bit-flip noise.
**The Pauli-Z gate (Z)** changes the phase of the ∣1⟩ state without altering measurement results. You'll find it often used to mimic phase-flip noise.
**The Hadamard gate (H)** creates superposition, making it possible for a qubit to reside in both ∣0⟩ and ∣1⟩ states at once.
**Rotation gates (RX, RY)** spin the qubit state around various axes of the Bloch sphere by an angle θ. Many variational quantum algorithms employ these adjustable gates widely.
Then there's the **CNOT gate**, a two-qubit gate which flips the target qubit if the control qubit is in the ∣1⟩ state. This one's crucial for generating entanglement and adding correlations between qubits.

In summary, these gates serve as the backbone of the quantum circuit we experiment with throughout the project.

---

## Entanglement

Entanglement is a key aspect of quantum mechanics where two or more qubits become intertwined and act as one big system. This feature is what gives quantum computing its edge over classical computing.

Entanglement is super important for several areas like quantum algorithms, quantum communication, quantum cryptography, quantum error correction, and quantum simulation.

One easy method to achieve entanglement is using a Hadamard gate followed by a CNOT gate. If you start with the state ∣00⟩, this process will result in the Bell state:

(|00⟩ + |11⟩)/√2
	​

In this state, measurements of the two qubits are perfectly correlated, demonstrating a hallmark feature of quantum entanglement.

In this project, entanglement is generated through CNOT gates within the experimental circuit. These gates create correlations between qubits, making the circuit sensitive to quantum noise and suitable for evaluating the performance of Zero-Noise Extrapolation (ZNE) and Richardson Extrapolation techniques.

---
## Quantum Circuits

A quantum circuit is a sequence of quantum gates applied to qubits in order to perform a computation. Similar to classical circuits, operations are executed from left to right, and measurements are performed at the end to obtain classical results.

In this project, a two-qubit variational circuit was used. The circuit combines rotation gates (RX and RY) with CNOT gates to prepare entangled quantum states that are sensitive to noise. This makes it a suitable benchmark for evaluating Quantum Error Mitigation techniques such as Zero-Noise Extrapolation (ZNE).

![Variational Circuit](images/1.png)

*Figure 1: Variational quantum circuit used in the experiments.*

---

## Why Are Quantum Computers Noisy?

Quantum computers, even though super powerful, are really finicky and get bothered by noise. This is because qubits need to keep delicate states like superposition and entanglement, which can get messed up easily by the outside world or hardware glitches.

The usual offenders causing all this trouble? Well, it's decoherence when qubits talk to the environment, imperfect actions during operations, and blunders when we measure them. As quantum circuits get more complex, these errors pile up and mess with the results we'd ideally want.

Since current tech can't rid of all the noise, scientists now aim to lessen its annoying effect. For example, Quantum Error Mitigation uses Zero-Noise Extrapolation to guess what the flawless result should look like. Because of all these issues, there's a big drive to figure out ways to make quantum computing smoother.


---
## The NISQ Era

Modern quantum computers go by the name **NISQ (Noisy Intermediate-Scale Quantum)**. These have anywhere from tens to hundreds of qubits, but the catch is that they're very noisy and prone to errors, making full fault-tolerant quantum computing impossible right now.

The NISQ era is a transition period in quantum computing. Even though we can run some cool quantum tasks, the results aren't always dependable due to that pesky noise, particularly in more complex circuits.

Because of this, a lot of research aims to boost NISQ device performance. Instead of waiting around for perfect quantum computers down the line, scientists are already figuring out ways to make the best of today's tech through Quantum Error Mitigation.

From there, a key technique called **Zero-Noise Extrapolation (ZNE)** comes into play. This is one of the most popular ways to cut down on the effects of noise in current systems.

---
## Quantum Error Correction vs Quantum Error Mitigation

Dealing with noise that messes up calculations is the big challenge in quantum computing. Scientists use two main methods to handle this problem.

First, there’s Quantum Error Correction (QEC). This approach protects quantum info by spreading a logical qubit across multiple physical ones. If errors occur, they can sometimes be spotted and corrected. That sounds fantastic! But here's the downside: QEC requires a bunch of extra qubits, which makes it pretty hard to put into practice with current tech.

Next, we’ve got Quantum Error Mitigation (QEM). Rather than trying to fix errors directly like QEC does, QEM tries to predict what results would be if the quantum machine was totally quiet. Since it doesn’t require as much, it actually works better with what we've got right now.

Because our present quantum machines suffer from noise and limitations, finding ways to mitigate these issues effectively has become super important. Folks have come up with various ideas for QEM, including Zero-Noise Extrapolation (ZNE), Probabilistic Error Cancellation (PEC), and Clifford Data Regression (CDR).

Among these, Zero-Noise Extrapolation (ZNE) seems to lead the pack. Many prefer it because it's fairly simple and works nicely with our currently noisy systems.


The difference between the two approaches can be summarized as follows:

| Quantum Error Correction                      | Quantum Error Mitigation                  |
| --------------------------------------------- | ----------------------------------------- |
| Attempts to correct errors                    | Attempts to reduce the impact of errors   |
| Requires many physical qubits                 | Requires little or no additional hardware |
| Long-term solution                            | Near-term solution                        |
| Suitable for fault-tolerant quantum computing | Suitable for NISQ devices                 |
| Hardware intensive                            | Computationally efficient                 |

---



# Related Work

Quantum Error Mitigation has really picked up steam because of the limits of noisy NISQ devices. One key method that scientists have looked at a lot is Zero-Noise Extrapolation (ZNE).

Temme, Bravyi, and Gambetta laid the groundwork for ZNE back in 2017. They figured out how to find noise-free expectation values by running quantum circuits at different noise levels and then extrapolating those results to what happens when there's no noise.

Li and Benjamin added to this in 2018, focusing on real-world strategies to boost accuracy on current quantum hardware. They stressed finding ways to improve results without using the costly process of full Quantum Error Correction.

Then came a big step forward: Digital Zero-Noise Extrapolation. This technique amplifies noise via circuit folding, not by fiddling with hardware settings directly. This made ZNE simpler to put into practice on existing machines – it's actually the approach we'll be using here.

And to help researchers run experiments, software like Mitiq was created. It offers hands-on applications of ZNE and other Quantum Error Mitigation methods.

---

## Position of This Work

This project evaluates the effectiveness of Zero-Noise Extrapolation (ZNE) under different quantum noise models. Specifically, it compares the performance of ZNE for:

- Depolarizing Noise
- Bit-Flip Noise
- Phase-Flip Noise

The study also investigates the difference between First-Order and Second-Order Richardson Extrapolation, providing insight into the benefits of higher-order error mitigation techniques.


### Depolarizing Noise

Depolarizing Noise models random quantum errors by applying Pauli X, Y, or Z errors with equal probability. As the noise level increases, the quantum state gradually loses information and approaches a completely mixed state.

:contentReference[oaicite:0]{index=0}

**Characteristics**
- Random quantum errors
- Affects both amplitudes and phases
- Common benchmark for simulations

### Bit-Flip Noise

Bit-Flip Noise is the quantum analogue of a classical bit error, causing a qubit state to flip between |0⟩ and |1⟩. It is modeled using the Pauli-X operator.

:contentReference[oaicite:1]{index=1}

**Characteristics**
- Changes the computational basis state
- Similar to classical bit inversion
- Easy to interpret and analyze


### Phase-Flip Noise

Phase-Flip Noise alters the phase of a quantum state without directly changing measurement probabilities. It is modeled using the Pauli-Z operator and can significantly affect quantum interference.

:contentReference[oaicite:2]{index=2}

**Characteristics**
- Preserves measurement probabilities
- Alters phase relationships
- Impacts interference-based computations



---

# Comparison of Noise Models

| Noise Model | Pauli Operator | Effect |
|-------------|---------------|---------|
| Depolarizing | X, Y, Z | Randomizes the quantum state |
| Bit-Flip | X | Flips |0⟩ and |1⟩ |
| Phase-Flip | Z | Changes the phase of the state |

---

# Zero-Noise Extrapolation (ZNE)

Zero-Noise Extrapolation (ZNE) is one of the most widely used Quantum Error Mitigation techniques for noisy quantum computers. Instead of correcting errors directly, ZNE estimates the result that would have been obtained on an ideal noise-free quantum computer.

The key idea is surprisingly simple: rather than attempting to remove noise, we intentionally increase it and observe how the circuit output changes. By analyzing the results at different noise levels, we can extrapolate back to the zero-noise limit.

The ZNE workflow consists of three steps:

1. Execute the quantum circuit at its original noise level.
2. Artificially amplify the noise and repeat the execution.
3. Apply an extrapolation method to estimate the noise-free result.

For sufficiently small noise levels, the expectation value can be approximated as:

where:

- \(E^{*}\) is the ideal noise-free expectation value.
- \(p\) is the noise strength.
- \(a_1, a_2, a_3,\ldots\) are unknown coefficients.

Since the expectation value varies smoothly with noise, measurements obtained at multiple noise levels can be used to estimate the value at \(p=0\), providing an approximation of the ideal quantum result.


---

## Noise Scaling and Circuit Folding

Zero-Noise Extrapolation requires measurements at multiple noise levels. Since quantum hardware does not usually allow direct control of noise strength, ZNE uses **Circuit Folding** to artificially amplify noise while preserving the circuit's logical behavior.

For a gate \(G\), folding replaces:

G

with:

G G† G

Since G†G = I (the identity operation), the logical computation remains unchanged while the circuit accumulates more noise.

Examples of circuit folding:

| Scale Factor | Circuit |
|-------------|---------|
| 1 | G |
| 3 | G G† G |
| 5 | G G† G G† G |

![Folded Circuit](images/3.png)

*Figure 4: Circuit folding used to amplify noise while preserving the logical computation.*

## Expectation Values and Richardson Extrapolation

After executing the circuit at different noise scales, expectation values are measured. In this project, the observable is:

O = Z ⊗ Z
The measured expectation values are then used to estimate the zero-noise result through Richardson Extrapolation.

### First-Order Richardson Extrapolation

Using measurements at scales 1 and 3:
E_ZNE^(1) = (3E₁ − E₃) / 2
This removes the dominant linear error term.

### Second-Order Richardson Extrapolation

Using measurements at scales 1, 3, and 5:
E_ZNE^(2) = (15E₁ − 10E₃ + 3E₅) / 8

This removes higher-order error terms and often provides a more accurate estimate of the ideal expectation value.

## Experimental Workflow

The workflow used in this project is:

1. Construct the variational quantum circuit.
2. Generate folded circuits with different noise scales.
3. Apply the selected noise model.
4. Measure expectation values.
5. Perform First-Order and Second-Order Richardson Extrapolation.
6. Compare the mitigated results with the ideal noise-free value.


# Experimental Setup

## Software Environment

The implementation was developed using:

- Python
- Qiskit
- Qiskit Aer
- NumPy
- Matplotlib

Qiskit Aer was used to simulate noisy quantum circuits and generate density matrices for evaluating expectation values and state fidelity.

---

## Variational Quantum Circuit

A two-qubit variational quantum circuit was used throughout the experiments. The circuit combines parameterized RX and RY rotation gates with CNOT gates to generate non-trivial quantum states and qubit correlations.

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
## Simulation Method

All noisy simulations were performed using the density matrix simulator available in Qiskit Aer. Density matrices were chosen because they can accurately represent noisy and mixed quantum states.

# Noise Models

Three noise models were investigated:

Depolarizing Noise
Bit-Flip Noise
Phase-Flip Noise

Noise probabilities ranging from 0.001 to 0.02 were considered, with additional experiments conducted at higher noise levels.

# Evaluation Metrics

Two metrics were used:

# State Fidelity

State fidelity was computed between the ideal and noisy quantum states to quantify the impact of noise.

# Expectation Value

The observable used throughout the experiments was

ZZ=Z⊗Z

with expectation value

E=Tr(ρZZ)

where ρ is the density matrix of the quantum state.

## Zero-Noise Extrapolation Setup

Noise scaling was performed using global circuit folding with scale factors:

s = 1
s = 3
s = 5

For a gate G, folding replaces

G→GG
†
G

thereby increasing the effective noise while preserving the logical computation.


## Richardson Extrapolation

Two extrapolation methods were evaluated:

First-Order Richardson Extrapolation using scales s=1 and s=3.
Second-Order Richardson Extrapolation using scales s=1, s=3, and s=5.

The performance of both methods was compared across all investigated noise models.

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



# Conclusion

This project investigated Zero-Noise Extrapolation (ZNE) as a practical Quantum Error Mitigation technique for noisy NISQ devices. A two-qubit variational quantum circuit was evaluated under Depolarizing, Bit-Flip, and Phase-Flip noise models using circuit folding and Richardson Extrapolation.

The results showed that ZNE consistently improved the accuracy of expectation value estimates across all investigated noise models. In particular, Second-Order Richardson Extrapolation achieved the best overall performance, providing significantly lower errors than both the original noisy measurements and First-Order extrapolation.

These findings demonstrate that meaningful improvements in quantum computation accuracy can be achieved without requiring additional qubits or full Quantum Error Correction, making ZNE a valuable tool for near-term quantum computing.

# Future Work

Several directions can extend this work:

- Evaluate ZNE on real quantum hardware such as IBM Quantum devices.
- Investigate additional noise models, including Amplitude Damping and Thermal Relaxation.
- Apply ZNE to larger and deeper quantum circuits.
- Compare ZNE with other Quantum Error Mitigation techniques such as Probabilistic Error Cancellation (PEC) and Clifford Data Regression (CDR).
- Explore machine learning approaches for modeling noise and improving extrapolation accuracy.

These extensions would provide a deeper understanding of the capabilities and limitations of Quantum Error Mitigation for future quantum computing systems.


# References

[1] K. Temme, S. Bravyi, and J. M. Gambetta, “Error Mitigation for Short-Depth Quantum Circuits,” Physical Review Letters, vol. 119, no. 18, 2017.

[2] A. He, B. Nachman, W. A. de Jong, and C. W. Bauer, “Zero-noise extrapolation for quantum-gate error mitigation with identity insertions,” Physical Review A, vol. 102, no. 1, 2020.

[3] P. Giurgica-Tiron et al., “Digital Zero Noise Extrapolation for Quantum Error Mitigation,” IEEE International Conference on Quantum Computing and Engineering (QCE), 2020.

[4] R. LaRose et al., “Mitiq: A software package for error mitigation on noisy quantum computers,” arXiv:2009.04417, 2020.

[5] Y. Li and S. C. Benjamin, “Practical Quantum Error Mitigation for Near-Future Applications,” Physical Review X, vol. 8, no. 3, 2018.



...
