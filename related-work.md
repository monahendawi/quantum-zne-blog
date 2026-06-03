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
