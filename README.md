# QuantumComputing

<script
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"
  type="text/javascript">
</script>


In this repository, I will be exploring quantum algorithms, refering mostly to the Nielsen&Chuang, "Learn Quantum Computing with Python and IBM Quantum Experience" and https://medium.com/qiskit/learn-quantum-computing-with-these-seven-projects-7478d90d125a

I have taken inspiration from https://medium.com/qiskit/learn-quantum-computing-with-these-seven-projects-7478d90d125a to build this repository, but have added algorithms from other sources that I will refer to in their respective sections.

## 0 Quantum Random Number Generator

The quantum random number generator is interesting when first working with quantum computers, as it exploits a fundamental property of quantum particles: they actually behave randomly. In fact, in our everyday life we never observe *true* randomness. Say, you're rolling a die. Is the outcome truly random? If you knew everything about the system - the weight of the die, its shape, the force you executed to spin it, its torque, air resistance and so on, you could theoretically predict exactly where the die will land every single time. It just appears like a random process because all that information is not available to us. This is reflected in classical random number generators, appropriately named pseudorandom number generators (PSRN), that generate number sequences through mathematical equations. One of the most commonly used is the linear congruential generator (LCG) $$X_{n+1}$$
