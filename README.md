# QuantumComputing


In this repository, I will be exploring some quantum algorithms, taking inspiration from different sources including the Nielsen, Chuang: "Quantum Computation and Quantum Information" (referred to as Mike&Ike), Loredo: "Learn Quantum Computing with Python and IBM Quantum Experience" (referred to as IBMbook), Bhattacharyya et al.: "Quantum Machine Learning" and some IBM Qiskit Tutorials provided in thei quantum lab. All notebooks are created on IBM's quantum computing lab, written in Qiskit. This repo requires some basic familiarity with quantum mechanics and quantum circuits. You should also be somewhat familiar with the standard Qiskit packages.

## 0 Entangled Qubits

Before diving into the Qiskit library, I tried to conduct a simple experiment on IBM's Quantum Composer. It is basically the simplest form of entaglement of two states. Both states start out in |0>, I apply a Hadamard gate to the top state to create a superposition state of equal amplitudes. To entangle the states, I apply a CNOT gate with the top state being the control qubit and the bottom state the target. When we now measure the top qubit, the bottom qubit must be in the same state and vice versa. 

![Circuit Composer](/images/entangledCoinsComposer.png) ![Histogram of Measured States](/images/entangledCoinsHistResized.png)

## 1 Quantum Random Number Generator

The quantum random number generator is interesting when first working with quantum computers, as it exploits a fundamental property of quantum particles: they actually behave randomly. In fact, in our everyday life we never observe *true* randomness. Say you're rolling a die. Is the outcome truly random? If you knew everything about the system - the weight of the die, its shape, the force you executed to spin it, its torque, air resistance and so on, you could theoretically predict exactly where the die will land every single time. It just appears like a random process because all that information is not available to us. This is reflected in classical random number generators, appropriately named pseudorandom number generators (PSRN). One of the most commonly used PSRN is the linear congruential generator (LCG), where X_{n+1} = (a X_n + c) mod m. By changing the values of m, n and c, you can change the way that the number is generated, typically by setting a seed, but it is evident that these are not truly random numbers. 

Quantum particles, however, are truly random. You can know everything about your system, and yet only be able to predict the probability of an outcome, never a concrete outcome. The way we will build a random number generator is very simple: We start out with a certain number of qubits, 4 in this case, apply a Hadamard gate to each one of them in order to create superposition states of equal amplitudes, and then we measure them all. For each qubit, there is a 50% chance of it being in state |0> after measurement, and a 50% chance of being in state |1>.

## 2 THE Teleportation Circuit

This was my first formal introduction to quantum computing, and is often the first quantum circuit that students learn about. You can find detailed explanations of the architecture in the Mike&Ike section 1.3.7. We create a quantum register with 3 qubits, the first of which is the unknows state (the one that Alice wants to transmit to Bob), the second and third qubits are the entangled EPR pair, the first of which belongs to Alice, and the second to Bob. We create the unknown state by applying a Pauli-X gate, followed by a Pauli-Z gate, following instructions from section 4 of the IBMbook, but you could apply other unitary transformations. 

## 3 Deutsch and Deutsch-Josza Algorithm

The Deutsch Algorithm and its extension to an n-qubit system is a staple quantum algorithm that employs quantum parallelism. Suppose we have a function f: {0, 1} -> {0, 1}, known as the oracle, and we dispose of a query qubit and a target (auxiliary) qubit. There are four possible configurations for f: f(0) = f(1) = 0 (constant 0), f(0) = f(1) = 1 (constant 1), f(0) = 0, f(1) = 1 (balanced), f(1) = 0, f(0) = 1 (balanced). To evaluate whether f is balanced or constant, classical computing would need to evaluate each case seperately. Using the principles of quantum parallelism, we can evaluate this with just one measurement. The Deutsch Algorithm allows us to determine the balanced/constant property by only measuring the state of the first qubit after a certain set of transformations (the circuit for an unbalanced oracle is depicted below):

![Deutsch Algorithm](/images/deutschCircuit.png)

