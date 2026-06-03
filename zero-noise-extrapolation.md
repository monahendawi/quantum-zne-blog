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

Zero-Noise Extrapolation (ZNE) is a Quantum Error Mitigation technique that attempts to estimate the result of an ideal noise-free quantum computation.

Instead of trying to eliminate noise from the hardware itself, ZNE studies how the output of a quantum circuit changes as the amount of noise increases.

By observing this behavior, it becomes possible to estimate what the result would have been if no noise were present.

The technique was first introduced by Temme, Bravyi, and Gambetta in 2017 and has since become one of the most influential methods in Quantum Error Mitigation research.

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

To perform extrapolation, measurements must be collected at multiple noise levels.

Unfortunately, on real quantum hardware it is usually impossible to directly modify the physical noise strength.

Instead, ZNE artificially amplifies the effective noise while preserving the logical computation.

This process is known as Noise Scaling.

The goal is not to change the quantum algorithm itself, but simply to make the circuit experience a larger amount of noise.

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
