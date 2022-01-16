# QuantumComputing


In this repository I will be collecting some of the quantum algorithms that I have experimented with, taking inspiration from different sources including the Nielsen, Chuang: "Quantum Computation and Quantum Information" (referred to as Mike&Ike), Loredo: "Learn Quantum Computing with Python and IBM Quantum Experience" (referred to as IBMbook), Bhattacharyya et al.: "Quantum Machine Learning" and some IBM Qiskit Tutorials provided in their quantum lab. All notebooks are created on IBM's quantum computing lab, written in Qiskit. This repo requires some basic familiarity with quantum mechanics and quantum circuits. You should also be somewhat familiar with the standard Qiskit packages. For now, I will not be providing thorough reviews of each algorithm but I might in the future.

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

The Deutsch-Josza algorithm is a natural extension to an n-qubit query register (still one auxiliary qubit) and it is here that we truly see the power of quantum parallelism: Denoting f as constant 0 (constant 1) if it always yields 0 (1) and as balanced if it yields 0 for half of the states and 1 for the other half, assuming that no other configurations are possible, and noting that an n-qubit system has 2^n possible configurations, it is easy to see that to evaluate the property of the oracle with classical computing, we would have to perform 2^(n-1) + 1 computations in the worst case, whereas the Deutsch-Josza algorithm only requires one measurement! 

## 4 Simon's Algorithm

The Deutsch-Josza Algorithm leverages phase kickback to differentiate between balanced and constant oracles by setting the auxiliary qubit to |1> at the beginning. 

Simon's Algorithm is what is known as a periodic quantum algorithm, as it is based on the quantum Fourier transform. It was the first algorithm to show exponential speed-up with respect to the best classical solution. The problem is to determine whether an oracle is one-to-one (injective) or two-to-one (the reciprocal image of each value in the function's range has exactly two elements in the function's domain). Similarly to the calculations from the previous section, it is clear that classically, at least 2^(n-1) + 1 computations must be performed. Simon's algorithm gurantees to find the solution in O(n) steps, achieving an exponential speedup. In order to compare the mappings, the auxiliary register must contain n qubits rather than 1. The entiree circuit thus contains 2n qubits.
Note that qiskit has already implemented Simon's oracle (from qiskit_textbook.tools import simon_oracle), but here I implemented the oracle from scratch.

## 5 Shor's Factoring Algorithm

## 6 Grover's Search Algorithm

## 7 Quantum Kernel Classification

In classical machine learning, kernel methods are frequently used in pattern recognition. The kernel trick allows us to transform complex data structures into higher dimensional Hilbert spaces where the data is linearly seperable, and support vector classifiers or regressors can be employed without having to evaluate the feature map at each data point. For highly complex structures however, even the kernel method can fail as the kernel function becomes too comutationally costly to evaluate. This is where quantum algorithms can outshine classical methods. Havlicek et al. present in "Supervised learning with quantum enhanced feature spaces" two methods on NISQ computers by representing the feature space as a quantum state. The one I have explored here is called "Quantum Kernel Estimation" and directly applies a classical SVM onto the data seperated through the feature map. In order for the methods to outperform the classical SVM, the feature map must be sufficiently complex. The authors of the paper propose to apply a Hadamard gate to all qubits, followed by a specific transformation that can be implemented by applying a CNOT gates and Z-gates, and repeating those two transformations once more. All qubits are initially in the sate |0>. The authorss also use data specifically generated to be fully linearly seperable after applying the feature map. Both the feature map and the data are available in the qiskit library.

The link between kernel methods and quantum machine learning models is discussed more in detail in Schuld: Quantum machine learning models are kernel methods

## 8 Quantum Neural Networks

Several models of a potential quantum neural net have been proposed, both on NISQ and fault-tolerant devices. For a global overview of some interesting approaches, see Schuld, Sinayskiy, Petruccione: The quest for a Quantum Neural Network.

A few challenges arise when attempting to translate the framework of classical neural networks to the quantum realm. First, quantum mechanics are inherently linear, which begs the question of how to implement non-linear activation functions. Another issue is that of parameter updates. In classical neural nets, parameter updates are typically done via some form of backpropagation. This approach becomes impossible in a quantum circuit, as it would require storing all intermediate states of the network during computation. 

One approach to tackle these issues and produce a quantum neural net on NISQ devices is known as the parameterised quantum circuit. The PQC is a hybrid classical-quantum model, integrating a quantum circuit into an otherwise classical framework. Data is prepared on a classical device, using well known data preprocessing methods. The output of this preprocessing is used as the parameters of the encoder circuit in the PQC. The encoder is followed by a variational circuit, itself followed by a measurement operation. From the measurements, expectation values of observables are estimated. These estimates are fed into a classical post-processing unit where a non-linear activation function can be applied as usual. 

![Architecture of a PQC](/images/PQC-schema.jpg)

Parameter updates are done by considering the quantum circuit as a black box and using the parameter shift rule. For a detailled derivation of the parameter shift rule, see Schuld et al., Evaluating analytic gradients on quantum hardware, and for a more complete overview of the structure of PQCs, see Benedetti et al., Parameterized quantum circuits as machine learning models.

Beer et al.: Training deep quantum neural networks
