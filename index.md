# Quantum Error Mitigation using Zero-Noise Extrapolation

## Abstract

Quantum computing has emerged as a promising computational paradigm capable of solving certain problems more efficiently than classical computers. However, current quantum devices operate in the Noisy Intermediate-Scale Quantum (NISQ) era, where noise and hardware imperfections significantly limit computational accuracy. Quantum Error Mitigation (QEM) techniques have therefore become essential for improving the reliability of near-term quantum computations.

This project investigates Zero-Noise Extrapolation (ZNE), one of the most widely used Quantum Error Mitigation techniques. A variational two-qubit quantum circuit was implemented using Qiskit and evaluated under three different noise models: Depolarizing Noise, Bit-Flip Noise, and Phase-Flip Noise. Noise amplification was achieved through Circuit Folding, while First-Order and Second-Order Richardson Extrapolation were used to estimate noise-free expectation values.

Experimental results demonstrate that Zero-Noise Extrapolation significantly reduces estimation errors across all investigated noise models. Furthermore, Second-Order Richardson Extrapolation consistently outperformed First-Order Richardson Extrapolation, achieving the highest mitigation accuracy. The study highlights the effectiveness of ZNE as a practical error mitigation strategy for current NISQ devices and demonstrates its potential for improving the reliability of near-term quantum computations.

---
# Introduction

Quantum computing has attracted significant attention in recent years due to its potential to solve computational problems that are challenging for classical computers. By exploiting the principles of quantum mechanics, such as superposition and entanglement, quantum computers can process information in fundamentally different ways from conventional computing systems. These unique capabilities have led researchers to explore quantum approaches for applications in cryptography, optimization, quantum chemistry, materials science, and machine learning.

Despite this promise, practical quantum computing remains limited by a fundamental challenge: noise. Unlike classical bits, quantum bits (qubits) are extremely sensitive to their surrounding environment. Small disturbances arising from hardware imperfections, environmental interactions, and measurement inaccuracies can alter quantum states and significantly degrade computational results. As quantum circuits become larger and deeper, these errors accumulate and increasingly affect the reliability of quantum computations.

Current quantum devices belong to what is commonly known as the Noisy Intermediate-Scale Quantum (NISQ) era. Although these systems contain enough qubits to perform meaningful computations, they are not yet capable of implementing large-scale fault-tolerant quantum algorithms. As a result, reducing the impact of noise has become one of the most important research challenges in modern quantum computing.

Traditionally, Quantum Error Correction (QEC) has been viewed as the long-term solution to quantum noise. However, QEC requires substantial hardware resources and a large number of physical qubits to protect quantum information effectively. Since these resources are not currently available on most NISQ devices, researchers have increasingly focused on Quantum Error Mitigation (QEM) techniques as practical alternatives for improving computational accuracy.

Among the various Quantum Error Mitigation approaches, Zero-Noise Extrapolation (ZNE) has emerged as one of the most popular and effective methods. Rather than correcting errors directly, ZNE estimates the result that would have been obtained in a noise-free environment by studying how measured quantities change as the effective noise level increases. This strategy allows improvements in computational accuracy without requiring additional logical qubits or fault-tolerant hardware.

The objective of this project is to investigate the effectiveness of Zero-Noise Extrapolation under multiple quantum noise models. Specifically, the study evaluates the performance of ZNE under Depolarizing Noise, Bit-Flip Noise, and Phase-Flip Noise using a variational quantum circuit implemented in Qiskit. Noise amplification is achieved through Circuit Folding, while both First-Order and Second-Order Richardson Extrapolation are applied to estimate noise-free expectation values.

By comparing the mitigation performance across different noise models and extrapolation orders, this work provides practical insight into the strengths and limitations of Zero-Noise Extrapolation for near-term quantum computing applications. The results demonstrate the potential of ZNE to improve computational accuracy and contribute to the ongoing effort to bridge the gap between current noisy hardware and future fault-tolerant quantum computers.

---



# Background

## Why Quantum Computing?

Almost every area of our lives has changed as a result of modern technology. Classical computers have become an indispensable component of contemporary culture, from smartphones and social media to scientific research and artificial intelligence.

Significant advancements have been made during the last few decades thanks to steadily rising processing power. Even with the most potent supercomputers in the world, some issues are still very challenging.

Think about the challenge of modeling a complicated molecule. The number of potential quantum states increases exponentially with the number of atoms. The computational resources needed eventually grow to the point that traditional computers are unable to carry out the simulation effectively.

Similar difficulties can be seen in other significant fields, such as:

* Drug discovery
* Materials science
* Optimization
* Cryptography
* Machine learning

These limitations motivated researchers to ask a fundamental question:

**Can we build computers that operate according to the laws of quantum mechanics rather than classical physics?**

Quantum computing was developed as a result of this concept.

Quantum computers, in contrast to classical computers, take advantage of special quantum phenomena like entanglement and superposition. These characteristics make it possible for quantum systems to handle information in essentially different ways, and they may offer notable computational advantages for particular problem classes.

Even though they are still in their infancy, quantum computing is one of the most fascinating fields of study in contemporary science and engineering.


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

## Superposition

One of the most remarkable features of quantum mechanics is a phenomenon known as **superposition**.

To understand superposition, let us first consider a classical bit.

A classical bit can only occupy one state at a time. At any given moment, it must be either:

* 0
* 1

There is no intermediate possibility.

A qubit, however, behaves differently.

Instead of being restricted to a single state, a qubit can exist in a combination of both states simultaneously. This is known as a **superposition state**.

For example, a qubit may be prepared in the state:

(|0⟩ + |1⟩)/√2

In this state, the qubit is not simply 0 and it is not simply 1. Instead, it contains information about both possibilities simultaneously.

When a measurement is performed, the quantum state collapses and produces one of the two possible outcomes:

* 0 with probability 50%
* 1 with probability 50%

Compared to traditional computing, this behavior is essentially different.

Imagining a spinning coin is a natural approach to conceptualize superposition.

Just as a classical bit is either 0 or 1, a coin on a table is either heads or tails.

But it's not obvious whether the coin is heads or tails while it's spinning. Aspects of both options are present in its current state. This comparison offers a helpful intuition for comprehending superposition, despite its flaws.

One of the primary ways quantum computers can interpret information differently from classical computers is through the creation and manipulation of superposition states.

In many quantum algorithms, qubits are first prepared in superposition states before operations that take advantage of the information stored in those states are carried out.


Unfortunately, superposition is also extremely fragile. Interactions with the environment can destroy these states, causing the quantum system to lose information. This phenomenon is one of the primary sources of noise in quantum computing and motivates the need for error mitigation techniques such as Zero-Noise Extrapolation.

---
## Quantum Gates

In classical computing, computations are performed using logic gates such as AND, OR, and NOT. These gates manipulate classical bits to perform calculations.

Quantum computers also use gates, but instead of acting on bits, they operate on qubits. These operations are known as **quantum gates**.

Quantum gates modify the quantum state of a qubit and are represented mathematically by unitary matrices. By applying sequences of quantum gates, it becomes possible to perform complex quantum computations.

In this project, several quantum gates are used to construct the experimental circuit. Before examining the circuit itself, it is useful to understand the purpose of these gates.

---

### Pauli-X Gate

The Pauli-X gate is often considered the quantum equivalent of the classical NOT gate.

Its action is simple:

|0⟩ → |1⟩

|1⟩ → |0⟩

In other words, it flips the state of the qubit.

This gate is particularly important because Bit-Flip Noise is mathematically modeled using the Pauli-X operator.

---

### Pauli-Z Gate

Unlike the Pauli-X gate, the Pauli-Z gate does not change the measured value of the qubit.

Instead, it changes the phase of the quantum state.

For example:

|0⟩ → |0⟩

|1⟩ → −|1⟩

Although this transformation may appear small, phase information plays a crucial role in many quantum algorithms.

Phase-Flip Noise is modeled using the Pauli-Z operator.

---

### Hadamard Gate

The Hadamard gate is one of the most important gates in quantum computing.

Its primary purpose is to create superposition.

For example:

|0⟩ → (|0⟩ + |1⟩)/√2

After applying a Hadamard gate, the qubit has an equal probability of being measured as 0 or 1.

Many quantum algorithms begin by placing qubits into superposition using Hadamard gates.

---

### Rotation Gates

Unlike Pauli gates, which perform fixed transformations, rotation gates allow continuous control of a qubit's state.

Two important rotation gates are:

* RX(θ)
* RY(θ)

where θ represents a rotation angle.

These gates rotate the quantum state around different axes of the Bloch Sphere.

Rotation gates are particularly useful in variational quantum algorithms because their parameters can be adjusted and optimized during computation.

The experimental circuit used in this project relies heavily on RX and RY gates to generate non-trivial quantum states.

---

### CNOT Gate

The Controlled-NOT (CNOT) gate is one of the most important two-qubit gates in quantum computing.

The gate operates using:

* A control qubit
* A target qubit

The target qubit is flipped only if the control qubit is in state |1⟩.

Unlike single-qubit gates, the CNOT gate can create entanglement between qubits.

Because entanglement is a key resource in quantum computing, the CNOT gate appears in many quantum algorithms and quantum communication protocols.

The circuit used in this project contains two CNOT gates that introduce correlations between the two qubits and make the circuit sensitive to quantum noise.

---

## Entanglement

If superposition is one of the fundamental principles of quantum computing, **entanglement** is often considered its most powerful resource.

Entanglement describes a unique quantum phenomenon in which two or more qubits become correlated in a way that cannot be explained by classical physics.

When qubits are entangled, the state of one qubit becomes directly related to the state of the other, regardless of the distance separating them.

This does not mean that information travels instantaneously between the qubits. Rather, it means that the quantum system must be described as a whole rather than as independent individual qubits.

---

### Why is Entanglement Important?

Many of the advantages offered by quantum computing arise from the ability to create and manipulate entangled states.

Entanglement plays a central role in:

* Quantum algorithms
* Quantum communication
* Quantum cryptography
* Quantum error correction
* Quantum simulation

Without entanglement, many quantum algorithms would lose their computational advantage over classical approaches.

---

### Creating Entanglement

One of the simplest ways to generate entanglement is by combining a Hadamard gate with a CNOT gate.

Consider a two-qubit system initially prepared in the state:

|00⟩

First, a Hadamard gate is applied to the first qubit, creating a superposition:

(|00⟩ + |10⟩)/√2

Next, a CNOT gate is applied.

The resulting state becomes:

(|00⟩ + |11⟩)/√2

This state is known as a **Bell State**, one of the most famous examples of quantum entanglement.

---

### Bell States

Bell states are maximally entangled two-qubit states.

The Bell state

(|00⟩ + |11⟩)/√2

has a remarkable property.

If the first qubit is measured and found to be 0, the second qubit will also be measured as 0.

If the first qubit is measured and found to be 1, the second qubit will also be measured as 1.

The outcomes are perfectly correlated.

These correlations cannot be explained using classical probability alone and are a direct consequence of quantum entanglement.

---

### Entanglement in This Project

The experimental circuit used in this project contains two CNOT gates.

These gates create correlations between the qubits and generate non-trivial quantum states that are sensitive to noise.

As a result, the expectation value measured in the experiments reflects not only the state of individual qubits but also the correlations established between them.

This makes the circuit a suitable testbed for evaluating the effectiveness of Zero-Noise Extrapolation and Richardson Extrapolation techniques.

---
## Quantum Circuits

Just as classical computers execute programs using sequences of logic gates, quantum computers perform computations using **quantum circuits**.

A quantum circuit is a graphical representation of a quantum computation, showing how quantum gates are applied to qubits over time.

In a quantum circuit:

* Horizontal lines represent qubits.
* Boxes represent quantum gates.
* Operations are applied from left to right.
* Measurements are usually performed at the end of the circuit.

A quantum algorithm can therefore be viewed as a sequence of quantum operations designed to transform an initial quantum state into a desired final state.

---

### Classical Circuits vs Quantum Circuits

Although quantum circuits may visually resemble classical logic circuits, there are important differences.

Classical circuits manipulate bits that are always either 0 or 1.

Quantum circuits manipulate qubits that can exist in superposition states and become entangled with one another.

As a result, quantum circuits can perform operations that have no classical equivalent.

---

### Building Quantum Algorithms

Quantum algorithms are typically constructed by combining multiple quantum gates.

For example:

* Hadamard gates create superposition.
* Rotation gates prepare specific quantum states.
* CNOT gates create entanglement.
* Measurements extract classical information from the quantum system.

By carefully arranging these operations, researchers can design circuits for a wide variety of applications, including optimization, machine learning, chemistry, and cryptography.

---

### The Circuit Used in This Project

To evaluate Zero-Noise Extrapolation, a two-qubit variational quantum circuit was constructed.

The circuit contains:

* RX rotation gates
* RY rotation gates
* CNOT gates

These gates generate non-trivial quantum states and create correlations between qubits, making the circuit sensitive to quantum noise.

The circuit was intentionally designed to include both single-qubit and two-qubit operations so that different types of noise could influence the computation.

This makes it an appropriate benchmark for studying Quantum Error Mitigation techniques such as Zero-Noise Extrapolation.



![Variational Circuit](images/1.png)

Figure 1: The variational quantum circuit used in the experiments.

---

### Why This Circuit?

A completely trivial circuit would not provide meaningful information about noise and error mitigation.

By introducing multiple parameterized rotations together with entangling gates, the circuit becomes sufficiently complex to exhibit realistic noise effects while remaining small enough to analyze and simulate efficiently.

The expectation values obtained from this circuit are later used to evaluate the effectiveness of Zero-Noise Extrapolation under different noise models.

---

## Why Are Quantum Computers Noisy?

Up to this point, quantum computing may appear extremely powerful. Quantum computers can exploit superposition, entanglement, and quantum interference to perform computations that are difficult for classical systems.

However, there is a major challenge that currently prevents quantum computers from reaching their full potential:

**Quantum noise.**

Unlike classical bits, qubits are extremely fragile. Their quantum states can be disturbed by even the smallest interactions with the surrounding environment.

As a result, maintaining accurate quantum information throughout a computation becomes a significant engineering challenge.

---

### Fragility of Quantum States

A classical bit can remain stored in memory for long periods without significant issues.

A qubit, however, must preserve delicate quantum properties such as superposition and entanglement.

Unfortunately, these properties can easily be destroyed.

Sources of disturbance include:

* Temperature fluctuations
* Electromagnetic interference
* Imperfect control electronics
* Hardware imperfections
* Interactions with surrounding particles

Even when these disturbances are very small, they can accumulate during circuit execution and significantly affect the final result.

---

### Decoherence

One of the most important sources of quantum noise is **decoherence**.

Decoherence occurs when a quantum system unintentionally interacts with its environment.

As this interaction takes place, the quantum system gradually loses the information stored in its superposition and entanglement states.

In simple terms, decoherence causes a quantum system to behave more like a classical system.

Because most quantum algorithms rely heavily on maintaining coherent quantum states, decoherence is one of the primary obstacles to reliable quantum computation.

---

### Gate Errors

Quantum computations are performed by applying quantum gates.

In an ideal world, every gate would be executed perfectly.

In practice, however, physical hardware is never perfect.

Small inaccuracies during gate implementation introduce errors into the quantum state.

As more gates are applied, these errors accumulate throughout the circuit.

This is particularly important because many useful quantum algorithms require long sequences of gate operations.

---

### Measurement Errors

At the end of a quantum computation, qubits are measured to obtain classical information.

Unfortunately, the measurement process itself is not error-free.

A qubit that should be measured as 0 may occasionally be reported as 1, and vice versa.

Although measurement errors are often smaller than other noise sources, they still contribute to the overall uncertainty of quantum computations.

---

### Impact of Noise

The presence of noise means that the result produced by a quantum computer may differ from the ideal theoretical result.

As circuit depth increases, noise accumulates and can eventually dominate the computation.

This limitation makes it difficult to execute large-scale quantum algorithms reliably on current hardware.

As a consequence, reducing the impact of noise has become one of the most important research topics in modern quantum computing.

The next section introduces the concept of NISQ devices and explains why error mitigation techniques have become essential for near-term quantum computers.


---
## The NISQ Era

Because of the noise challenges discussed in the previous section, modern quantum computers are often described as **NISQ devices**.

NISQ stands for:

**Noisy Intermediate-Scale Quantum**

This term was introduced to describe the current generation of quantum computers, which contain tens to hundreds of qubits but still suffer from significant levels of noise.

Although these devices represent a major technological achievement, they are not yet capable of performing large-scale fault-tolerant quantum computation.

---

### What Does "Noisy" Mean?

The word "Noisy" refers to the fact that quantum operations are imperfect.

Every quantum computation is affected by:

* Decoherence
* Gate errors
* Measurement errors
* Environmental interactions

As the number of operations increases, the accumulated noise also increases.

This means that deeper quantum circuits generally produce less reliable results.

---

### What Does "Intermediate-Scale" Mean?

The term "Intermediate-Scale" refers to the number of available qubits.

Current quantum processors contain significantly more qubits than the earliest experimental devices.

However, they still possess far fewer qubits than would be required for large-scale fault-tolerant quantum computing.

For example, many practical quantum algorithms may eventually require thousands or even millions of high-quality logical qubits, while current devices typically operate with only tens or hundreds of noisy physical qubits.

---

### Why Is the NISQ Era Important?

The NISQ era represents a transitional stage in the development of quantum computing.

Researchers can already run useful quantum circuits and explore practical applications. However, hardware limitations prevent the execution of many large-scale algorithms.

As a result, improving the reliability of NISQ devices has become one of the most active research areas in quantum computing.

---

### The Central Challenge

The fundamental challenge of the NISQ era can be summarized as follows:

Quantum computers are already powerful enough to perform interesting computations, but they are still too noisy to consistently produce ideal results.

This creates a gap between theoretical quantum algorithms and practical hardware implementations.

Bridging this gap is one of the primary motivations behind quantum error suppression techniques.

The next question is therefore:

**How can we reduce the impact of noise without waiting for fully fault-tolerant quantum computers?**


---
## Quantum Error Correction vs Quantum Error Mitigation

Once researchers recognized that noise is one of the primary obstacles to practical quantum computing, an important question emerged:

**How can we reduce the impact of quantum noise?**

Over the years, two major approaches have been developed:

1. Quantum Error Correction (QEC)
2. Quantum Error Mitigation (QEM)

Although both approaches aim to improve the reliability of quantum computations, they operate in fundamentally different ways.

---

### Quantum Error Correction (QEC)

Quantum Error Correction (QEC) is a collection of techniques designed to protect fragile quantum information from the effects of noise and hardware imperfections.

In classical computing, error correction is relatively straightforward. If a bit is accidentally flipped from 0 to 1, redundancy can be used to detect and correct the mistake. Quantum systems, however, present a much greater challenge. Because quantum information cannot be copied arbitrarily and because measurements disturb quantum states, protecting quantum information requires specialized techniques.

The main idea behind Quantum Error Correction is to encode a single logical qubit into multiple physical qubits. By distributing information across several qubits, it becomes possible to detect and correct certain errors without directly measuring the encoded quantum state.

For many researchers, Quantum Error Correction represents the ultimate solution to quantum noise. In principle, a sufficiently large fault-tolerant quantum computer could perform long computations while continuously correcting errors as they occur.

Unfortunately, implementing QEC requires a very large number of physical qubits, making it impractical for most current quantum devices.

---

### Why Is Quantum Error Correction Difficult?

Although QEC is theoretically powerful, it comes with a substantial cost.

A single logical qubit may require many physical qubits for reliable protection.

In large-scale fault-tolerant quantum computers, the number of required physical qubits can become extremely large.

As a result, current NISQ devices generally lack the hardware resources necessary to fully implement quantum error correction.

For this reason, QEC is often viewed as a long-term objective rather than an immediate solution.

---

### Quantum Error Mitigation (QEM)

While quantum error correction attempts to actively detect and correct errors, quantum error mitigation follows a different philosophy.

Instead of eliminating noise directly, error mitigation techniques attempt to estimate what the ideal noise-free result would have been.

In other words, QEM does not remove errors from the hardware itself. Rather, it reduces their impact on the final computation.

This approach is particularly attractive because it can often be applied without requiring additional logical qubits.

---

### Why Error Mitigation Matters in the NISQ Era

Current quantum hardware is noisy, but it is already capable of executing useful circuits.

Waiting for fully fault-tolerant quantum computers may take many years.

Therefore, researchers have focused on developing practical techniques that can improve accuracy using today's hardware.

Quantum Error Mitigation has emerged as one of the most promising approaches for achieving this goal.

Several mitigation techniques have been proposed, including:

* Zero-Noise Extrapolation (ZNE)
* Probabilistic Error Cancellation (PEC)
* Clifford Data Regression (CDR)
* Symmetry Verification

Among these methods, Zero-Noise Extrapolation has become one of the most widely used techniques because of its simplicity and compatibility with current quantum devices.

---

### Error Correction vs Error Mitigation

The difference between the two approaches can be summarized as follows:

| Quantum Error Correction                      | Quantum Error Mitigation                  |
| --------------------------------------------- | ----------------------------------------- |
| Attempts to correct errors                    | Attempts to reduce the impact of errors   |
| Requires many physical qubits                 | Requires little or no additional hardware |
| Long-term solution                            | Near-term solution                        |
| Suitable for fault-tolerant quantum computing | Suitable for NISQ devices                 |
| Hardware intensive                            | Computationally efficient                 |

---

### Why This Project Focuses on Error Mitigation

Because current quantum computers belong to the NISQ era, implementing large-scale quantum error correction remains impractical.

For this reason, this project focuses on Quantum Error Mitigation, specifically Zero-Noise Extrapolation (ZNE), as a practical method for improving computational accuracy without requiring additional qubits.

The next section introduces the fundamental principles behind Zero-Noise Extrapolation and explains why it has become one of the most influential error mitigation techniques in modern quantum computing.

---
## Why Zero-Noise Extrapolation?

At this stage, we understand that modern quantum computers are powerful but noisy.

We also know that large-scale quantum error correction remains impractical for current NISQ devices.

This naturally leads to an important question:

**If we cannot completely eliminate noise, can we still estimate what the correct result should have been?**

Zero-Noise Extrapolation (ZNE) was developed to answer exactly this question.

Rather than attempting to remove noise from the hardware, ZNE estimates the result that would have been obtained if the quantum computation had been executed in a perfectly noise-free environment.

---

### An Intuitive Example

Imagine taking a photograph through a slightly dirty camera lens.

The resulting image is blurry.

Now imagine taking the same photograph again using an even dirtier lens.

The image becomes even more distorted.

If we repeat this process several times using different levels of distortion, we may begin to understand how the image changes as the amount of blur increases.

Using this information, it becomes possible to estimate what the original clean image looked like before any distortion was introduced.

Zero-Noise Extrapolation follows a very similar philosophy.

Instead of increasing image blur, we intentionally increase quantum noise and observe how the measured result changes.

These measurements are then used to estimate the value that would have been obtained in the absence of noise.

---

### The Core Idea

The central idea of Zero-Noise Extrapolation can be summarized in three steps:

1. Execute the quantum circuit under its normal noise level.
2. Artificially amplify the noise and execute the circuit again.
3. Use the collected measurements to estimate the zero-noise result.

Importantly, ZNE does not require additional logical qubits or fault-tolerant hardware.

This makes it particularly attractive for current NISQ quantum computers.

---

### Why Is ZNE Popular?

Zero-Noise Extrapolation has become one of the most widely studied Quantum Error Mitigation techniques because it offers several advantages:

* It is relatively simple to implement.
* It requires no additional logical qubits.
* It can be applied to existing quantum hardware.
* It is compatible with a wide range of quantum algorithms.
* It often provides significant accuracy improvements.

For these reasons, ZNE has become a standard benchmark technique in the field of Quantum Error Mitigation.

In the following sections, we will explore how noise can be artificially amplified and how extrapolation techniques can be used to estimate noise-free quantum results.


# Related Work

The challenge of quantum noise has motivated extensive research into Quantum Error Mitigation techniques over the past decade. Among the proposed approaches, Zero-Noise Extrapolation has emerged as one of the most influential and widely adopted methods for improving the accuracy of computations performed on NISQ devices.

Rather than relying on large-scale Quantum Error Correction, Zero-Noise Extrapolation attempts to estimate the result of an ideal quantum computation by studying how expectation values change under increasing levels of noise. This idea has inspired a substantial body of research and has become a cornerstone of modern Quantum Error Mitigation.

---

## Error Mitigation for Short-Depth Quantum Circuits

The foundations of Zero-Noise Extrapolation were established by Temme, Bravyi, and Gambetta in their pioneering 2017 work *Error Mitigation for Short-Depth Quantum Circuits*.

In this paper, the authors introduced the idea of deliberately amplifying noise and then extrapolating the measured expectation values back to the zero-noise limit. Their work demonstrated that meaningful improvements in computational accuracy could be achieved without requiring full Quantum Error Correction.

This contribution is widely regarded as one of the most important milestones in the development of Quantum Error Mitigation and forms the theoretical foundation of the present project.

---

## Practical Quantum Error Mitigation

In 2018, Li and Benjamin further explored practical error mitigation strategies for near-term quantum devices.

Their work emphasized the importance of developing techniques that can be implemented on noisy quantum hardware without requiring excessive computational resources. The study highlighted the growing need for mitigation methods that could bridge the gap between ideal quantum algorithms and the limitations of NISQ hardware.

The ideas presented in this work helped establish Quantum Error Mitigation as a practical alternative to full Quantum Error Correction for near-term quantum computing applications.

---

## Digital Zero-Noise Extrapolation

A major advancement in the field was introduced by Giurgica-Tiron and collaborators through the concept of Digital Zero-Noise Extrapolation.

One of the main challenges in implementing ZNE is the inability to directly control physical noise levels on quantum hardware. To overcome this limitation, the authors proposed circuit folding techniques that artificially increase the effective noise experienced by a circuit while preserving its logical computation.

This approach has become one of the most widely used implementations of Zero-Noise Extrapolation and serves as the primary noise-scaling strategy adopted in this project.

---

## Software Frameworks for Error Mitigation

As Quantum Error Mitigation gained popularity, several software frameworks were developed to facilitate experimental research.

One of the most notable examples is Mitiq, an open-source software package specifically designed for Quantum Error Mitigation. Mitiq provides implementations of Zero-Noise Extrapolation, Probabilistic Error Cancellation, and other mitigation techniques.

Such frameworks have significantly accelerated research in the field by providing standardized tools for evaluating mitigation strategies across different quantum platforms.

---

## Position of This Work

Building upon the existing literature, this project focuses on evaluating the effectiveness of Zero-Noise Extrapolation under multiple quantum noise models.

While many studies demonstrate the general effectiveness of ZNE, this work provides a comparative analysis of:

* Depolarizing Noise
* Bit-Flip Noise
* Phase-Flip Noise

In addition, the project investigates the relative performance of First-Order and Second-Order Richardson Extrapolation, providing insight into the benefits of higher-order error mitigation strategies.

By combining multiple noise models with multiple extrapolation orders, the study offers a practical perspective on the strengths and limitations of Zero-Noise Extrapolation in realistic noisy quantum environments.

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


# Zero-Noise Extrapolation (ZNE)

## Why Do We Need Zero-Noise Extrapolation?

In the previous sections, we learned that quantum computers are extremely sensitive to noise.

Even when a quantum algorithm is theoretically correct, the result obtained from a real quantum device may differ significantly from the ideal answer because of decoherence, gate imperfections, and measurement errors.

This creates a major challenge:

**How can we estimate the result that would have been obtained on a perfect noise-free quantum computer?**

One possible solution is Quantum Error Correction. However, as discussed earlier, current NISQ devices do not possess enough resources to implement large-scale fault-tolerant quantum computation.

As a result, researchers have developed alternative approaches known as Quantum Error Mitigation techniques.

Among these techniques, Zero-Noise Extrapolation (ZNE) has emerged as one of the most practical and widely used methods.

---

## What is Zero-Noise Extrapolation?

Zero-Noise Extrapolation (ZNE) is one of the most widely used Quantum Error Mitigation techniques for noisy quantum computers.

The primary objective of ZNE is to estimate the result that would have been obtained if the quantum computation had been executed on a perfectly noise-free quantum computer.

Unlike Quantum Error Correction, ZNE does not attempt to actively detect or correct errors during execution. Instead, it studies how the output of a quantum circuit changes as noise increases and then uses this information to infer the ideal result.

This approach is particularly attractive for NISQ devices because it requires little additional hardware and can often be implemented directly on existing quantum processors.

Since its introduction by Temme, Bravyi, and Gambetta in 2017, Zero-Noise Extrapolation has become one of the most influential error mitigation techniques in modern quantum computing research.

---

## The Counterintuitive Idea Behind ZNE

At first glance, ZNE may seem strange.

If noise is harmful, why would we intentionally increase it?

The answer lies in understanding how scientists often study complex systems.

Imagine taking a photograph through a slightly dirty camera lens.

The image appears blurry.

Now imagine taking the same photograph using an even dirtier lens.

The image becomes more distorted.

If we repeat this process several times and observe how the image changes, we may be able to estimate what the original clean image looked like.

Zero-Noise Extrapolation follows exactly the same philosophy.

Rather than trying to directly remove noise, we intentionally increase it and study how the measured result changes.

These measurements are then used to infer the result corresponding to zero noise.

---

## The Core Idea of ZNE

The complete Zero-Noise Extrapolation process can be summarized in three steps:

1. Execute the quantum circuit at its normal noise level.
2. Artificially amplify the noise and execute the circuit again.
3. Use extrapolation techniques to estimate the noise-free result.

The key observation is that noise affects the measured expectation value in a predictable way when the noise level remains sufficiently small.

---

## Why Does ZNE Work?

Suppose that the measured expectation value depends on the noise strength p.

Instead of directly obtaining the ideal value, we observe:

E(p)

For sufficiently small noise levels, the expectation value can be approximated using a Taylor expansion:

E(p)=E* + a₁p + a₂p² + a₃p³ + ...

where:

* E* is the ideal noise-free value.
* p represents the noise strength.
* a₁, a₂, a₃ are unknown coefficients.

The important observation is that the expectation value changes smoothly as noise increases.

Because of this smooth behavior, measurements collected at different noise levels can be used to estimate the value of the function when the noise strength becomes zero.

---

## Understanding the Linear Approximation

Near the zero-noise region, the expectation value can often be approximated by a low-order polynomial.

This assumption is the foundation of Zero-Noise Extrapolation.

The figure below illustrates this idea.

![Linear Approximation](images/2.png)

Figure 3: Approximation of the expectation value as a smooth function of noise strength.

Although we cannot directly access the point corresponding to zero noise, we can estimate it using nearby noisy measurements.

---
## Noise Scaling

A central requirement of Zero-Noise Extrapolation is the ability to observe how a quantum computation behaves under different noise levels.

Ideally, we would like to execute the same quantum circuit multiple times while gradually increasing the physical noise present in the hardware. Unfortunately, most quantum processors do not provide direct control over their underlying noise sources.

To overcome this limitation, ZNE relies on a technique known as Noise Scaling.

The goal of Noise Scaling is not to modify the quantum algorithm itself. Instead, it artificially amplifies the effective noise experienced by the circuit while preserving its logical behavior.

By generating several versions of the same computation that experience different amounts of noise, researchers can observe how the measured expectation value changes and use this information to estimate the zero-noise result.
---

## Circuit Folding

In this project, Noise Scaling is achieved using Circuit Folding.

The idea is surprisingly simple.

Consider a quantum gate G.

Instead of executing:

G

we execute:

G G† G

where G† is the inverse of G.

Because:

G†G = I

the overall logical operation remains unchanged.

Therefore:

G G† G = G

Mathematically, both circuits perform exactly the same computation.

However, the folded circuit contains more physical operations.

Since every physical operation introduces noise, the folded circuit accumulates a larger amount of noise.

This allows us to generate multiple effective noise levels without modifying the underlying hardware.

The circuit-folding strategy used in this project follows the Digital Zero-Noise Extrapolation framework proposed in the literature.

![Folded Circuit](images/3.png)

Figure 4: Circuit folding used to amplify noise while preserving the logical computation.

---

## Noise Scaling Factors

Several scaling factors can be generated using circuit folding.

Scale = 1

Original circuit

Scale = 3

G G† G

Scale = 5

G G† G G† G

As the scale factor increases, the effective noise level also increases.

In this project, the following scaling factors were used:

* Scale 1
* Scale 3
* Scale 5

---

## Expectation Values

After executing the circuit at different noise scales, expectation values are measured.

The expectation value of an observable O is written as:

E = ⟨O⟩

In this project, the observable used is:

O = Z ⊗ Z

which measures the correlation between the two qubits.

These expectation values form the data used for extrapolation.

---

## Why Richardson Extrapolation?

Once measurements have been collected at multiple noise levels, we need a mathematical procedure that estimates the value corresponding to zero noise.

Richardson Extrapolation provides exactly this capability.

The technique combines measurements obtained at different noise scales in a way that cancels the dominant noise contributions.

As a result, the estimated value becomes significantly closer to the ideal noise-free result.

---

## First-Order Richardson Extrapolation

Using measurements obtained at scaling factors:

* s = 1
* s = 3

the first-order estimate is computed as:

E_ZNE^(1) = (3E₁ − E₃) / 2

This removes the dominant linear error term and provides a more accurate estimate than the original noisy measurement.

---

## Second-Order Richardson Extrapolation

Using measurements obtained at:

* s = 1
* s = 3
* s = 5

the second-order estimate becomes:

E_ZNE^(2) = (15E₁ − 10E₃ + 3E₅) / 8

Second-order extrapolation removes additional error terms and generally produces a more accurate estimate of the ideal expectation value.

However, because it relies on more measurements, it may also become more sensitive to statistical fluctuations.

---

## Complete Workflow

The complete Zero-Noise Extrapolation workflow used in this project is summarized below:

1. Construct the quantum circuit.
2. Execute the original circuit.
3. Generate folded versions of the circuit.
4. Apply the selected noise model.
5. Measure the expectation values.
6. Perform First-Order Richardson Extrapolation.
7. Perform Second-Order Richardson Extrapolation.
8. Compare the mitigated results with the ideal noise-free value.

This workflow forms the foundation of all experiments presented in this project.

---

## Why ZNE is Important

Zero-Noise Extrapolation has become one of the most influential Quantum Error Mitigation techniques because it offers several advantages:

* No additional qubits are required.
* Compatible with current NISQ devices.
* Simple to implement.
* Effective on both simulators and real hardware.
* Can significantly improve computational accuracy.

For these reasons, ZNE remains one of the most practical approaches for improving quantum computations before large-scale fault-tolerant quantum computers become available.


# Experimental Setup

## Overview

After introducing the theoretical foundations of Zero-Noise Extrapolation, the next step is to evaluate its effectiveness in practice.

The objective of this project is not only to implement ZNE, but also to understand how well it performs under different noise conditions. To achieve this goal, a controlled experimental environment was constructed using quantum circuit simulation.

The experiments were designed to answer three main questions.

First, how strongly do different noise models affect the outcome of a quantum computation?

Second, can Zero-Noise Extrapolation successfully recover results that are closer to the ideal noise-free values?

Finally, does Second-Order Richardson Extrapolation provide a measurable improvement over the simpler First-Order approach?

To answer these questions, a series of experiments were conducted using Qiskit and Qiskit Aer simulators, allowing complete control over the quantum circuit, the noise model, and the mitigation strategy.

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

## Quantum Circuit

Selecting an appropriate quantum circuit is an important part of any error mitigation study. If the circuit is too simple, the impact of noise may be difficult to observe. On the other hand, if the circuit becomes excessively large, the analysis becomes more complicated and computationally expensive.

For this reason, a two-qubit variational quantum circuit was designed for the experiments.

The circuit contains parameterized RX and RY rotation gates together with CNOT gates that create correlations between the two qubits. This combination provides a useful balance between simplicity and complexity. The circuit is small enough to be simulated efficiently while still exhibiting non-trivial quantum behavior.

The use of rotation gates allows the preparation of a wide variety of quantum states, while the CNOT gates introduce entanglement and make the circuit more sensitive to noise. Because the objective of this project is to study how noise affects quantum computations, it is important that the circuit contains both single-qubit and two-qubit operations.

As noise accumulates throughout the execution of the circuit, changes in the measured expectation values can be directly observed and analyzed using Zero-Noise Extrapolation.

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

## Why Use Density Matrices?

In an ideal quantum simulation, the state of a quantum system can often be represented using a state vector. However, once noise is introduced, the situation becomes more complicated.

Noise causes the quantum system to interact with its environment, leading to a loss of information and the creation of mixed states. Such states can no longer be described accurately using a single state vector.

To properly model noisy quantum computations, this project uses density matrices instead of pure state vectors.

Density matrices provide a more general mathematical framework that can represent both pure quantum states and mixed quantum states. This makes them particularly suitable for studying realistic noisy quantum systems.

For this reason, all noisy simulations in this project were executed using the density matrix simulator available in Qiskit Aer.


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

## Fidelity Evaluation

Before applying error mitigation techniques, it is useful to quantify how strongly noise affects the quantum state itself.

To achieve this, state fidelity was computed between the ideal quantum state and the noisy quantum state generated by simulation.

Fidelity can be interpreted as a measure of similarity between two quantum states. A fidelity value close to one indicates that the noisy state remains very similar to the ideal state, whereas lower fidelity values indicate stronger degradation caused by noise.

Although the primary goal of this project is to recover accurate expectation values, fidelity provides an important preliminary indicator of how severely each noise model disturbs the underlying quantum state.


---


## Expectation Value Measurement

While fidelity provides information about the similarity between quantum states, Zero-Noise Extrapolation is ultimately concerned with recovering accurate observable quantities.

For this reason, the experiments focus on measuring the expectation value of the observable Z ⊗ Z.

This observable measures the correlation between the two qubits and is particularly suitable for circuits containing entangling operations such as CNOT gates.

The choice of Z ⊗ Z is important because it captures information about the collective behavior of the two-qubit system rather than the state of an individual qubit.

Expectation values were computed from the density matrix generated by the noisy simulation. By comparing the expectation values obtained before and after mitigation, it becomes possible to directly evaluate the effectiveness of Zero-Noise Extrapolation.

The observable used throughout the experiments is

$$
ZZ = Z \otimes Z
$$

and the corresponding expectation value is computed as

$$
E = Tr(\rho ZZ)
$$

where $\rho$ denotes the density matrix of the noisy quantum state.
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
![Folded Circuit](images/3.png)

Figure 2: Example of circuit folding used to amplify noise while preserving the logical computation.
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

Quantum noise remains one of the most significant challenges facing modern quantum computing. Although quantum computers possess remarkable computational capabilities, the presence of noise limits their ability to produce accurate and reliable results.

This project investigated Zero-Noise Extrapolation (ZNE) as a practical Quantum Error Mitigation technique for improving the accuracy of computations performed on NISQ devices. Unlike Quantum Error Correction, which requires substantial hardware resources, ZNE provides a lightweight alternative that can be applied directly to existing quantum systems.

To evaluate the effectiveness of ZNE, a variational two-qubit quantum circuit was implemented and tested under three different noise models: Depolarizing Noise, Bit-Flip Noise, and Phase-Flip Noise. Noise amplification was achieved using Circuit Folding, while Richardson Extrapolation was employed to estimate the zero-noise expectation values.

The experimental results demonstrated that Zero-Noise Extrapolation consistently improved the accuracy of the measured expectation values across all investigated noise models. In every experiment, both First-Order and Second-Order Richardson Extrapolation reduced the estimation error relative to the original noisy measurements.

Among the evaluated approaches, Second-Order Richardson Extrapolation achieved the best overall performance. The largest improvement was observed under Depolarizing Noise, where the estimation error was reduced by approximately 115 times compared to the unmitigated result.

These findings confirm that Zero-Noise Extrapolation is an effective and practical mitigation strategy for current noisy quantum devices. The results also highlight the importance of higher-order extrapolation techniques when attempting to recover accurate quantum observables from noisy computations.

Overall, this study demonstrates that meaningful improvements in computational accuracy can be achieved without requiring additional qubits or full fault-tolerant quantum hardware, making Zero-Noise Extrapolation a valuable tool for near-term quantum computing applications.

# Future Work

While the results obtained in this project are encouraging, several opportunities remain for extending and improving the study.

First, the experiments were conducted using simulated noise models. Although simulation provides a controlled environment for evaluating mitigation techniques, real quantum hardware often exhibits more complex and hardware-specific noise characteristics. Future work could therefore investigate the performance of Zero-Noise Extrapolation on actual IBM Quantum devices.

Second, this project focused on three commonly used noise models: Depolarizing Noise, Bit-Flip Noise, and Phase-Flip Noise. Additional studies could explore more realistic noise processes such as Amplitude Damping, Thermal Relaxation, and correlated multi-qubit noise.

Another promising direction involves applying Zero-Noise Extrapolation to larger and deeper quantum circuits. As circuit complexity increases, noise accumulation becomes more severe, providing a valuable opportunity to evaluate the scalability of error mitigation techniques.

Future research could also compare Zero-Noise Extrapolation with other Quantum Error Mitigation approaches, including Probabilistic Error Cancellation, Clifford Data Regression, and Symmetry Verification. Such comparisons would provide a broader understanding of the strengths and limitations of different mitigation strategies.

Finally, machine learning techniques could be integrated with Quantum Error Mitigation to automatically model noise behavior and improve extrapolation accuracy. The combination of artificial intelligence and quantum error mitigation represents an exciting research direction for future quantum computing systems.

As quantum hardware continues to advance, practical error mitigation techniques such as Zero-Noise Extrapolation are expected to play an increasingly important role in bridging the gap between current NISQ devices and future fault-tolerant quantum computers.


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

# References

[1] K. Temme, S. Bravyi, and J. M. Gambetta, “Error Mitigation for Short-Depth Quantum Circuits,” Physical Review Letters, vol. 119, no. 18, 2017.

[2] A. He, B. Nachman, W. A. de Jong, and C. W. Bauer, “Zero-noise extrapolation for quantum-gate error mitigation with identity insertions,” Physical Review A, vol. 102, no. 1, 2020.

[3] P. Giurgica-Tiron et al., “Digital Zero Noise Extrapolation for Quantum Error Mitigation,” IEEE International Conference on Quantum Computing and Engineering (QCE), 2020.

[4] R. LaRose et al., “Mitiq: A software package for error mitigation on noisy quantum computers,” arXiv:2009.04417, 2020.

[5] Y. Li and S. C. Benjamin, “Practical Quantum Error Mitigation for Near-Future Applications,” Physical Review X, vol. 8, no. 3, 2018.


















antum Error Mitigation

...
