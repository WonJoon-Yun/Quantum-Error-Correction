<!-- ## Technical Jargons Used in this document:

1. Hypergraph
 - vertex: A vertex corresponds to a single check instance $C^i_t$ (i.e., check i evaluated over a specific time interval t). In practice, a vertex is the spacetime label (i,t) for a check outcome.
 - hyperedge:
2. Check
 - Detection event: if check =1 -->

 

## Without Transversal CNOT (Memory Test)

1. *Raw Stabilizer Measurement*

    | Time | Z1   | Z2   |
    | ---- | ---- | ---- |
    | 0    |  +1  | +1   |
    | 1    |  -1  | +1   |
    | 2    |  +1  | +1   |

2. *Check*
    When there is no *transversal CNOT*, each check is defined as the product of consecutive measurements of the *same* stabilizer:
    $C^i_t = Z^i_{t} \cdot Z^i_{t-1}$ such that $i\in {1,2}$ and $t\in {1,2}$.
    | Time | C1   | C2   |
    | ---- | ---- | ---- |
    | 1    |  -1 $Z^1_1 \cdot Z^1_0$ | +1  $Z^2_1 \cdot Z^2_1$    |
    | 2    |  -1  $Z^1_2 \cdot Z^1_2$ | +1   $Z^2_2 \cdot Z^2_2$  |


## With Transversal CNOT 


1. **Raw Stabilizer Measurement (Same as previous one)**

    | Time | Z1   | Z2   |
    | ---- | ---- | ---- |
    | 0    |  +1  | +1   |
    | 1    |  -1  | +1   |
    | 2    |  +1  | +1   |


2. **Check**
    Check with transversal CNOT is based on the back-propagating the stabilizer operator. 
    For example, you have two logical qubits (say, qubit 1 and 2) and apply transversal CNOT (1,2) at time between t=1 and t=2.
    The $Z_1$ stabilizer is unchanged by the CNOT, so, $C^1_1 = Z^1_1 \cdot Z^1_0$, and $C^1_2 = Z^1_2 \cdot Z^1_1$.
    The check of logical qubit 2 at the time $t+1$ is affected by transversal CNOT, which is written as $C^2_{t+1} = (Z^1_{t}  \cdot Z^2_{t}) \cdot Z^2_{t+1}$. Under a CNOT (1,2), the stabilizer transforms as $Z_2 \;\mapsto\; Z_1 Z_2$. Therefore, the check at time t=2 for logical qubit 2 must be defined as $\boxed{C^2_2 = (Z^1_1 \cdot Z^2_1)\cdot Z^2_2}$. Finally, the checks represented as follows:
    | Time |  C1  |  C2  |
    | ---- | ---- | ---- |
    | 1    |  -1 $Z^1_1 \cdot Z^1_0$ | +1 $Z^2_1 \cdot Z^2_0$  |
    | 2    |  -1 $Z^1_2 \cdot Z^1_1$ | -1 $(Z^1_1 \cdot Z^2_1) \cdot Z^2_2$  | 

**Note.** Conventionally, **single physical fault flips at most two checks**. However, a **single measurement error with transversal CNOT** on $Z_1$ at $t=1$ flips three checks $\{ C^1_1,\; C^1_2,\; C^2_2 \}$.
Since MWPM also assumes that **each physical fault flips at most two checks**, it cannot represent this error mechanism exactly and therefore cannot perform maximum-likelihood decoding for this circuit without approximation. To achieve fault tolerance it requires additional syndrome extraction rounds.
<!-- 
## Why correlated decoding requires only one round?
When the observed syndrome is exactly those three checks, the correlated decoder can explain it with one fault. No extra syndrome rounds are required because the model already contains the correct single-fault explanation. -->

<!-- 

2. Cor

One line of summary:

The fundanemtal unit of time required to reliably execute a single logical operation.

Technical writing:

(single logical qubit)
Syndrome extraction is fragile and has to be fault-tolerant.
each syndrome extraction has 2-4 cnots and 1 measurment operations.
1 qec cycle/round indicates a period of single syndrome extraction.
it has to be fault-tolerant, so it has to be repeated 'd' rounds to detect measurement and gate errors in syndrome extraction.

(multiple logical qubits?)
... (what is operation between logical qubits?)
(what is lattice surgery? why is it needed?)
why 'd' rounds are needed to operate multi-logical qubit operations?

what is correlated decoding? why is it needed?

Thus, entangling gates based on lattice surgery and standard error correction requires d rounds of syndrome extraction to ensure fault tolerance to measurement errors.

Minimum Weight Perfect Matching (MWPM) decoder assumes that error is propagated pairwise (order: 2). 
However, transversal CNOT has an error characteristic that is propagate deterministically, which means the error is propagated to three directions.
Correlated decoder is to decode this error charcterization efficiently.
By doing this, correlated decoder can detect measurement errors using less syndrome extraction rounds.

Why is d syndrome extraction round still needed for memory test?

- The space/time error -->
