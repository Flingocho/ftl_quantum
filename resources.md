# OpenQASM Codes for IBM Quantum Composer

This collection contains OpenQASM codes ready to use in the [IBM Quantum Composer](https://quantum-computing.ibm.com/composer).

---

## ⚖️ Deutsch-Jozsa Algorithm - Balanced Oracle

Implementation of the Deutsch-Jozsa algorithm with a **balanced oracle** (returns 0 for half of the inputs and 1 for the other half).

```qasm
OPENQASM 2.0;
include "qelib1.inc";

qreg q[4];
creg c[3];

// ------------------
// Initialization
// ------------------
reset q[0];
reset q[1];
reset q[2];
reset q[3];

// Superposition on inputs
h q[0];
h q[1];
h q[2];

// Ancilla in |−⟩
x q[3];
h q[3];

// ------------------
// BALANCED ORACLE
// ------------------
cx q[0], q[3];
cx q[1], q[3];
cx q[2], q[3];

// ------------------
// Interference
// ------------------
h q[0];
h q[1];
h q[2];

// Measurement ONLY of inputs (not ancilla)
measure q[0] -> c[0];
measure q[1] -> c[1];
measure q[2] -> c[2];
```

**Expected result:** Measurement different from `|000⟩` → **BALANCED** function

---

## 🔄 Deutsch-Jozsa Algorithm - Constant Oracle

Implementation of the Deutsch-Jozsa algorithm with a **constant oracle** (always returns 0 or always 1 for all inputs).

```qasm
OPENQASM 2.0;
include "qelib1.inc";

qreg q[4];
creg c[3];

// ------------------
// Initialization
// ------------------
reset q[0];
reset q[1];
reset q[2];
reset q[3];

// Superposition on inputs
h q[0];
h q[1];
h q[2];

// Ancilla in |−⟩
x q[3];
h q[3];

// ------------------
// CONSTANT ORACLE
// f(x) = 0 for all x
// (does nothing)
// ------------------

// ------------------
// Interference
// ------------------
h q[0];
h q[1];
h q[2];

// Measurement ONLY of inputs (not ancilla)
measure q[0] -> c[0];
measure q[1] -> c[1];
measure q[2] -> c[2];
```

**Expected result:** Measurement = `|000⟩` → **CONSTANT** function

---

## 🔍 Grover Algorithm - 3 Qubits → Marked State |101⟩

Implementation of Grover's algorithm to search for state `|101⟩` in a 3-qubit search space.

```qasm
OPENQASM 2.0;
include "qelib1.inc";

qreg q[3];
creg c[3];

// ------------------
// Initialization
// ------------------
reset q[0];
reset q[1];
reset q[2];

// Superposition
h q[0];
h q[1];
h q[2];

// ------------------
// ORACLE: mark |101⟩
// ------------------
// |101⟩ → q0=1, q1=0, q2=1
x q[1];

h q[2];
ccx q[0], q[1], q[2];
h q[2];

x q[1];

// ------------------
// DIFFUSION (Grover Diffusion)
// ------------------
h q[0];
h q[1];
h q[2];

x q[0];
x q[1];
x q[2];

h q[2];
ccx q[0], q[1], q[2];
h q[2];

x q[0];
x q[1];
x q[2];

h q[0];
h q[1];
h q[2];

// Measurement
measure q[0] -> c[0];
measure q[1] -> c[1];
measure q[2] -> c[2];
```

---

## 📚 Notes

- **Grover**: Amplifies the amplitude of the marked state. Requires approximately $\sqrt{N}$ iterations.
- **Deutsch-Jozsa**: Determines whether a function is constant or balanced in **a single oracle query** (vs $2^{n-1}+1$ classical queries).
- These codes can be copied directly into IBM Quantum Composer for visualization and execution.

## 🔗 Useful Links

- [IBM Quantum Composer](https://quantum-computing.ibm.com/composer)
- [OpenQASM Documentation](https://qiskit.github.io/openqasm/)
- [Qiskit Documentation](https://qiskit.org/documentation/)
