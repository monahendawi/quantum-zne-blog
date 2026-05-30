# Conclusion

Quantum noise remains one of the primary challenges preventing current quantum computers from achieving reliable large-scale computation. While Quantum Error Correction provides a long-term solution, its substantial hardware requirements make it difficult to deploy on today's Noisy Intermediate-Scale Quantum (NISQ) devices.

In this project, Zero-Noise Extrapolation (ZNE) was investigated as a practical Quantum Error Mitigation technique that can improve computational accuracy without requiring additional logical qubits.

Three different quantum noise models were evaluated:

- Depolarizing Noise
- Bit-Flip Noise
- Phase-Flip Noise

Noise amplification was achieved through circuit folding, and both First-Order and Second-Order Richardson Extrapolation were implemented to estimate noise-free expectation values.

The experimental results demonstrated that:

- Quantum noise significantly degrades circuit performance.
- Zero-Noise Extrapolation successfully reduces estimation errors.
- Richardson Extrapolation provides meaningful improvements over noisy measurements.
- Second-Order Richardson Extrapolation consistently outperforms First-Order Richardson Extrapolation.
- Phase-flip noise exhibited the largest improvement when higher-order extrapolation was applied.

Overall, the results confirm that Zero-Noise Extrapolation is an effective and practical error mitigation strategy for current NISQ quantum devices.

---

# Future Work

Several directions can be explored in future studies:

- Investigating larger quantum circuits.
- Evaluating additional noise models such as amplitude damping noise.
- Studying adaptive extrapolation techniques.
- Combining Zero-Noise Extrapolation with other Quantum Error Mitigation methods.
- Applying ZNE on real quantum hardware instead of simulation.

As quantum hardware continues to improve, Quantum Error Mitigation techniques such as Zero-Noise Extrapolation are expected to play an increasingly important role in enabling useful quantum computations before fault-tolerant quantum computers become available.
