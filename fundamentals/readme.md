# Quantum Error Correction

## What is quantum error correction?
Quantum error correction (QEC) is a technique that protects quaantum information from errors. 

## Why is it needed?
QEC is crucial in quantum computers which are error-prone. Running a quantum algorithm in quantum computers are also erroneous. QEC makes running quantum algorithm fault-tolerant.


# Quantum Error Correcting Code (QECC)

## 1. Formal Definition of QECC
A QECC is formally defined as a subspace $\mathcal{C}\subset(\mathbb{C}^2)^{\xdot n} with $dim(\mathcal{C})=2^k$ where $n$, $k$, $\mathcal{C}$ stand for the number of physical (data) qubits, number of logical qubits and the codespace, respectively.

### Characterization of QECC
QeCC is conventionally denoted as $[[n,k,d]]$ or [[n,k,d_x,d_z]], where
| Symbol | Meaning                              | What it counts                      |
| ------ | ------------------------------------ | ----------------------------------- |
| $n$    | Number of **data (physical) qubits** | Actual hardware qubits              |
| $k$    | Number of **logical qubits**         | Encoded qubits carrying information |
| $d$    | **Code distance**                    | Error-correction strength           |
| $d_x$    | **Code distance** for X errors                   | Error-correction strength           |
| $d_z$    | **Code distance**  for Z erros                  | Error-correction strength           |


- Data (physical) qubits ($n$)
  - These are the physical qubits used to encode the logical information
  - They are subject to noise, loss, decoherence, etc.

- Logical qubits
  - These are the encoded qubits after applying the code.
  - Each logical qubit is represented by a highly entangled state of the data qubit
  - Example: $k=12$ means 12 logical qubits are encoded simultaneously.

- Logical block
  - A logical block is one instance of the code applied to a fixed set of data qubits
  - One logical block contains $n$ data qubits, encodes $k$ logical qubits, detects up to $d-1$ errors, and corrects up to $\lfloor \frac{d-1}{2}\rfloor$ errors ($d-1$ erasures).

#### Characteristics of QECC that cannot be characterized by $n,k$, and $d$:

- check weight: the number of data qubits involved in the check

#### Example of [[144,12,12]]
| Property                 | Value                        |
| ------------------------ | ---------------------------- |
| Distance                 | (d = 12)                     |
| Detectable errors        | up to 11                     |
| Correctable Pauli errors | (\lfloor(12-1)/2\rfloor = 5) |
| Correctable erasures     | up to 11                     |



### Steps of QECC
#### Encoding
The encoding is an isometry which is expressed as $\mathcal{E}: (\mathbb{C}^2)^{\xdot k} \to (\mathbb{C}^2)^{\xdot n} such that $\mathcal{E}(|\psi_L\rangle)\in \mathcal{C}$.

#### Error-correction condition (Knill-Laflamme)
Let $\{E_a\}$ be a set of possible error operators on $n$ qubits.
The subspace $\mathcal{C}$ is a QECC for errors $\{E_a\}$ iff $\langle i_L | E_a^\dag E_b | j_L\rangle = C_{ab}\delta_ij$ for all logical basis states $|i_L\rangle$, $|j_L\rangle$ \in \mathcal{C}$.

##### The logical basis state $i_L\rangle$ is highly entangled state of $n$ physical qubits i.e., $|i_L\rangle \in \mathcal{C} = \{ |0_L\rangle, ... , |(2^k-1)_L\rangle\}$.

##### Takeaway
Logical basis states are encoded basis vectors whose relative geometry must be preserved under errors.The Knill–Laflamme condition enforces that all correctable errors act identically on the logical subspace, up to a label that can be measured and reversed.