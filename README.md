# QuantumComputing


In this repository, I will be exploring quantum algorithms, refering mostly to the Nielsen&Chuang, "Learn Quantum Computing with Python and IBM Quantum Experience" (which I will be referring to as IBMbook). All notebooks are created on IBM's quantum computing lab, written in Qiskit. This repo assumes that you have some basic familiarity with quantum mechanics and have seen a few simple quantum circuits before. You should also be somewhat familiar with the standard Qiskit packages.

I have taken inspiration from https://medium.com/qiskit/learn-quantum-computing-with-these-seven-projects-7478d90d125a to build this repository, but have added algorithms from other sources that I will refer to in their respective sections.

## 0 Entangled Qubits

Before diving into the Qiskit library, I tried to conduct a simple experiment on IBM's Quantum Composer. It is basically the simplest form of entaglement of two states. Both states start out in |0>, I apply a Hadamard gate to the top state to create a superposition state of equal amplitudes. To entangle the states, I apply a CNOT gate with the top state being the control qubit and the bottom state the target. When we now measure the top qubit, the bottom qubit must be in the same state and vice versa.

## 1 Quantum Random Number Generator

The quantum random number generator is interesting when first working with quantum computers, as it exploits a fundamental property of quantum particles: they actually behave randomly. In fact, in our everyday life we never observe *true* randomness. Say you're rolling a die. Is the outcome truly random? If you knew everything about the system - the weight of the die, its shape, the force you executed to spin it, its torque, air resistance and so on, you could theoretically predict exactly where the die will land every single time. It just appears like a random process because all that information is not available to us. This is reflected in classical random number generators, appropriately named pseudorandom number generators (PSRN). One of the most commonly used PSRN is the linear congruential generator (LCG) X_{n+1} = (a X_n + c) mod m. By changing the values of m, n and c, you can change the way that the number is generated, typically by setting a seed, but it is evident that these are not truly random numbers. 

Quantum particles, however, are truly random. You can know everything about your system, and yet only be able to predict the probability of an outcome, never a concrete outcome. The way we will build a random number generator is very simple: We start out with a certain number of qubits, 16 in this case, apply a Hadamard gate to each one of them in order to create superposition states of equal amplitudes, and then we measure them all. For each qubit, there is a 50% chance of it being in state |0> after measurement, and a 50% chance of being in state |1>. Note that the numbers are not exactlyy 50/50  in practice, as the quantum computer is not (yet) fault tolerant.

## 2 THE Teleportation Circuit

This was my first formal introduction to quantum computing, and is often the first quantum circuit that students learn about. You can find detailled explanations of the architecture in the Mike&Ike section 1.3.7. We create a quantum register with 3 qubits, the first of which is the unknows state (the one that Alice wants to transmit to Bob), the second and third qubits are the entangled EPR pair, the first of which belongs to Alice, and the second to Bob. We create the unknown state by applying a Pauli-X gate, followed by a Pauli-Z gate, following instructions from section 4 of the IBMbook, but you could apply other unitary transformations. 

## 3 Deutsch and Deutsch-Josza Algorithm

The Deutsch Algorithm and its extension to an n-qubit system is a staple quantum algorithm that employs quantum parallelism.
