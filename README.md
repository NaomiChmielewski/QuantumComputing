# QuantumComputing


In this repository, I will be exploring quantum algorithms, refering mostly to the Nielsen&Chuang, "Learn Quantum Computing with Python and IBM Quantum Experience" and https://medium.com/qiskit/learn-quantum-computing-with-these-seven-projects-7478d90d125a

I have taken inspiration from https://medium.com/qiskit/learn-quantum-computing-with-these-seven-projects-7478d90d125a to build this repository, but have added algorithms from other sources that I will refer to in their respective sections.

## 0 Quantum Random Number Generator

The quantum random number generator is interesting when first working with quantum computers, as it exploits a fundamental property of quantum particles: they actually behave randomly. In fact, in our everyday life we never observe *true* randomness. Say you're rolling a die. Is the outcome truly random? If you knew everything about the system - the weight of the die, its shape, the force you executed to spin it, its torque, air resistance and so on, you could theoretically predict exactly where the die will land every single time. It just appears like a random process because all that information is not available to us. This is reflected in classical random number generators, appropriately named pseudorandom number generators (PSRN). One of the most commonly used PSRN is the linear congruential generator (LCG) X_{n+1} = (a X_n + c) mod m. By changing the values of m, n and c, you can change the way that the number is generated, typically by setting a seed, but it is evident that these are not truly random numbers. 

Quantum particles, however, are truly random. You can know everything about your system, and yet only be able to predict the probability of an outcome, never a concrete outcome. The way we will build a random number generator is very simple: We start out with a certain number of qubits, 16 in this case, apply a Hadamard gate to each one of them in order to create superposition states of equal amplitudes, and then we measure them all. For each qubit, there is a 50% chance of it being in state |0> after measurement, and a 50% chance of being in state |1>. Note that the numbers are not exactlyy 50/50  in practice, as the quantum computer is not (yet) fault tolerant.
