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
