# Quantum Computing for IR and Optimization

## Basics of Quantum Computing
Quantum computing manipulates quantum systems using **qubits** (2-dimensional quantum systems). Unlike classical bits, qubits can exist in superposition, allowing for massive parallelism.
- **Challenges:** Decoherence and noise.

## Quantum Annealing (QA)
Quantum Annealing is a specialized form of quantum computing used for optimization problems. It is a relaxation of **Adiabatic Quantum Computing**.

### Key Concepts
- **Adiabatic Theorem:** A system in its ground state remains in that state if the Hamiltonian changes sufficiently slowly.
- **Quantum Tunnelling:** Allows the system to transition directly between states even if there is a high energy barrier, unlike classical paths that must go "over" the barrier.
- **Adiabatic Evolution:** The process of slowly evolving the system toward the global minimum (the solution).

## QUBO (Quadratic Unconstrained Binary Optimization)
Most optimization problems for QA are formulated as **QUBO** problems:
$$\text{argmin } x^T Q x$$
where $x$ is a vector of binary decision variables and $Q$ is a square matrix of constraints.

## Hardware Constraints: Minor Embedding
Since physical Quantum Processing Units (QPUs) have a specific topology (e.g., square), and QUBO problems may have different topologies (e.g., triangle), **Minor Embedding** is required.
- **Process:** Adding auxiliary variables (new nodes and edges) to map the problem's logical topology onto the QPU's physical topology while maintaining the same values.
