# TP
# Load Flow Analysis in Radial Distribution Systems with Distributed Generators (DGs)

This repository contains the **MATLAB implementation** of a **novel algorithm** for solving **power flow (PF) problems** in **radial distribution networks** integrated with **distributed generation (DG) units**.  
The algorithm is based on **graph theory** and **matrix algebra**, combined with the **Backward-Forward Sweep (BFS)** approach, to achieve **highly efficient and robust load flow solutions** for three-phase unbalanced distribution systems.

---

## **📌 Project Overview**

Traditional power flow algorithms like **Newton-Raphson** and **Gauss-Seidel** are effective for transmission systems but **struggle with distribution networks** due to:
- High **R/X ratio** of lines
- **Unbalanced loads** (star/delta configurations)
- **Mutual coupling** between phases
- Large number of nodes/buses

Our approach overcomes these limitations by:
1. Representing the network using **topological matrices** (Connectivity Matrix, Bus-Branch Topology Matrix).
2. Using **matrix operations** to significantly reduce computation complexity.
3. Integrating **DGs as PV buses**, with a reactive current injection strategy to maintain bus voltages.
4. Handling **all load types**: Constant Power (P), Constant Current (I), Constant Impedance (Z).

---

## **✨ Key Features**
- Supports **three-phase radial distribution networks**.
- Efficient **Backward-Forward Sweep using matrices**.
- Models **Distributed Generators (DGs)** as PV buses with voltage regulation.
- Handles both **star** and **delta** load configurations.
- **High convergence speed** due to reduced sequential computations.
- Scalable to large, complex networks.

---

## **🧮 Methodology**

### 1. **System Representation Using Matrices**
The algorithm relies on two main matrix categories:

| **Matrix Type** | **Purpose** |
|-----------------|-------------|
| **Topology Matrices** (e.g., Connectivity Matrix `E`, Bus-Branch Topology Matrix `T`) | Define the structure and connections of the network. |
| **Computation Matrices** (e.g., Branch Current Matrix `J`, Voltage Drop Matrix `D`, Source-to-Bus Voltage Drop Matrix `L`) | Used in iterative calculations for voltage and current updates. |

---

### 2. **Backward-Forward Sweep (BFS) with Matrix Algebra**
Instead of iterative node-by-node calculations, the algorithm performs **matrix multiplications**, which:
- Reduce computational time.
- Efficiently handle sparsity and large systems.
- Improve convergence speed.

**Steps:**
1. Initialize network matrices (`E`, `T`, `Z`, `S`).
2. Compute **branch currents** and **bus voltages** iteratively.
3. Check convergence threshold (e.g., 0.01% voltage deviation).
4. If DGs are present:
   - Treat DG buses as PQ buses initially.
   - After convergence, compute required **reactive current injections** to maintain DG bus voltage setpoints.

---

### 3. **Current Injection for DGs**
DGs are modeled as **PV buses**.  
The algorithm calculates **reactive current injections** to regulate voltage without affecting real power output using:

\[
I = Y \cdot V
\]

Where:
- `I` = Reactive current injection  
- `Y` = Admittance matrix  
- `V` = Voltage magnitude deviation

---

## **📊 Dataset Used**
The implementation uses a **modified IEEE 25-Bus System**, with:
- Balanced three-phase configuration.
- Mix of star and delta loads.
- Integration of DG units at selected buses.

---

## **💻 Implementation Details**

- **Language/Tool:** MATLAB  
- **Input Files:** Network data including:
  - Bus data
  - Branch data
  - Load specifications
  - DG locations and setpoints
- **Output Files:**
  - Bus voltage profiles (per phase)
  - Branch current flows
  - Convergence plots

### Example Output:
- **Voltage vs Bus Number** plots for all three phases.
- Reactive current injection analysis for DGs.

---

## **📈 Results**
The proposed method shows:
- **Faster convergence** compared to traditional BFS.
- Reduced **computational complexity** through optimized matrix operations.
- Accurate modeling of DGs and unbalanced loads.

**Sample Observation:**
- For the 25-bus test case, bus voltages converged within a 0.01% threshold in significantly fewer iterations.

---

## **📂 Repository Structure**
