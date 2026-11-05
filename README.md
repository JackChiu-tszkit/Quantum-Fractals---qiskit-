# Quantum Fractals: Julia Sets from One- and Two-Qubit States

A Python and Jupyter Notebook research project exploring how quantum-state amplitudes can be used to generate **Julia set fractals**.

The project uses **Qiskit**, **NumPy**, and **Matplotlib** to construct quantum circuits, simulate quantum states, generate fractal visualizations, and compare simulation results with measurements obtained from IBM Quantum hardware.

## Features

- Interactive quantum circuit construction using Qiskit
- Support for one-qubit and two-qubit quantum systems
- Quantum state visualization using Bloch spheres and Q-spheres
- Quantum statevector simulation
- Conversion of quantum amplitudes into complex Julia set parameters
- Fractal generation using NumPy and Matplotlib
- Execution on real IBM Quantum hardware
- Comparison of simulated and hardware-adjusted fractal images

## Technology Stack

- **Programming Language:** Python
- **Quantum Computing:** Qiskit
- **Quantum Hardware:** IBM Quantum
- **Numerical Computing:** NumPy
- **Data Visualization:** Matplotlib
- **Development Environment:** Jupyter Notebook
- **Interactive Circuit Design:** IBM Quantum CircuitComposer

## Project Structure

```text
Quantum-Fractals/
├── QFractals1qubit_v3.ipynb
├── QFractals2qubits_v3.ipynb
└── README.md
```

### QFractals1qubit_v3.ipynb

Generates Julia set fractals using quantum-state amplitudes from a single-qubit circuit.

The notebook:
1. Creates an interactive single-qubit quantum circuit.
2. Visualizes the quantum state on a Bloch sphere.
3. Executes the circuit using a statevector simulator.
4. Extracts the complex amplitudes.
5. Calculates the Julia set parameter.
6. Generates the corresponding fractal.
7. Executes the circuit on IBM Quantum hardware.
8. Compares simulated and hardware-adjusted fractal results.

### QFractals2qubits_v3.ipynb

Extends the approach to a two-qubit quantum system.

The notebook:
1. Creates an interactive two-qubit quantum circuit.
2. Visualizes the quantum state using a Q-sphere.
3. Simulates the quantum statevector.
4. Extracts four complex amplitudes.
5. Calculates the Julia set parameter using amplitude ratios.
6. Generates the corresponding fractal.
7. Executes the circuit on IBM Quantum hardware.
8. Compares the simulated and hardware-adjusted results.

## Mathematical Background

### Julia Set

A Julia set is generated through repeated iteration of the complex quadratic function:

```text
z(n+1) = z(n)^2 + c
```

where:

- `z` is a complex number.
- `c` is a constant complex parameter.
- `n` represents the iteration number.

Different values of `c` produce different fractal patterns.

In this project, the parameter `c` is derived from quantum-state amplitudes.

### One-Qubit Quantum State

A general single-qubit state is represented as:

```text
|ψ⟩ = a₀|0⟩ + a₁|1⟩
```

The Julia set parameter is calculated as:

```text
c = a₀ / a₁
```

The real and imaginary components are rounded to two decimal places. If the denominator is zero, the notebook sets `c = 0`.

### Two-Qubit Quantum State

A general two-qubit state is represented as:

```text
|ψ⟩ = a₀₀|00⟩ + a₀₁|01⟩ + a₁₀|10⟩ + a₁₁|11⟩
```

The notebook calculates:

```text
z₁ = a₀₀ / a₁₁
z₂ = a₀₁ / a₁₀

c = z₁ / z₂
```

The calculated complex parameter determines the resulting Julia set.

## Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Quantum-Fractals
```

### 2. Create a Python Environment

```bash
python -m venv .venv
```

Activate the environment:

**Windows:**

```bash
.venv\Scripts\activate
```

**macOS / Linux:**

```bash
source .venv/bin/activate
```

### 3. Install Dependencies

The project requires:

- Python
- Jupyter Notebook or JupyterLab
- NumPy
- Matplotlib
- Qiskit
- Qiskit Aer
- IBM Quantum integration
- IBM Quantum Widgets

**Compatibility Notice:** The notebooks use legacy Qiskit APIs, including `IBMQ`, `execute`, and `CircuitComposer`. They may not run with current Qiskit releases without modifications. Use a compatible legacy environment or migrate the code to modern Qiskit APIs.

## Usage

### 1. Start Jupyter Notebook

```bash
jupyter notebook
```

### 2. Open a Notebook

Choose one of the following:

```text
QFractals1qubit_v3.ipynb
QFractals2qubits_v3.ipynb
```

### 3. Configure IBM Quantum

The notebooks use the legacy IBM Quantum account interface:

```python
from qiskit import IBMQ

IBMQ.load_account()
```

An IBM Quantum account and compatible authentication configuration are required for the original account-loading and hardware execution cells.

### 4. Construct a Quantum Circuit

Use the interactive CircuitComposer to design a quantum circuit.

The notebooks support:

- Single-qubit circuits
- Two-qubit circuits
- Quantum state visualization
- Statevector simulation

### 5. Generate Julia Set Fractals

After obtaining the quantum-state amplitudes, the notebooks calculate the complex parameter `c` and generate a Julia set.

Example:

```python
plt.imshow(julia_set(c=z), cmap="magma")
plt.show()
```

The default rendering resolution is 1000 × 1000 pixels, with a maximum of 100 iterations.

### 6. Execute on Real Quantum Hardware

The notebooks identify a least-busy operational IBM Quantum backend with sufficient qubits.

Each experiment uses:

```python
shotno = 1024
```

Measurement counts are converted into observed probabilities and used to adjust the simulated amplitudes.

### 7. Compare Results

The notebooks visualize:

- Julia sets generated from simulated quantum-state amplitudes
- Julia sets generated from measurement-adjusted amplitudes

Example:

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 12))

axes[0].imshow(julia_set(c=z), cmap="magma")
axes[1].imshow(julia_set(c=zqc), cmap="magma")

plt.show()
```

## Quantum Hardware Measurement

The notebooks compare simulated state probabilities with observed measurement frequencies from IBM Quantum hardware.

The amplitude adjustment follows the approximate relationship:

```text
adjusted_amplitude =
    simulated_amplitude × sqrt(observed_probability / simulated_probability)
```

The adjusted amplitudes are then used to recalculate the Julia set parameter.

**Important:** Computational-basis measurements do not provide complete quantum-state information, including relative phases. This method is a heuristic adjustment of simulated amplitudes, not full quantum state tomography.

## Visualization

The project uses Matplotlib to render fractal patterns.

The Julia set function supports the following parameters:

| Parameter | Description | Default |
|-----------|-------------|---------|
| c | Complex Julia set parameter | Quantum-derived |
| height | Image height | 1000 |
| width | Image width | 1000 |
| x | Horizontal center | 0 |
| y | Vertical center | 0 |
| zoom | Zoom level | 1 |
| max_iterations | Maximum iterations | 100 |

Example:

```python
plt.imshow(
    julia_set(
        c=-0.4 + 0.6j,
        zoom=2,
        max_iterations=150
    ),
    cmap="magma"
)

plt.show()
```

## Limitations

- The notebooks depend on legacy Qiskit APIs.
- Circuit construction requires the interactive CircuitComposer widget.
- Certain amplitude ratios may be undefined when denominators are zero.
- Missing measurement outcomes may cause dictionary lookup errors.
- Hardware measurement frequencies cannot reconstruct quantum-state phases.
- Rounding complex amplitude ratios may significantly affect fractal patterns.
- Real quantum hardware execution depends on IBM Quantum availability and access permissions.

## Future Improvements

- Migrate to modern Qiskit and IBM Quantum Runtime.
- Add reproducible quantum circuit examples.
- Improve numerical stability and zero-denominator handling.
- Add automated fractal image exports.
- Support additional quantum circuit configurations.
- Improve simulator-versus-hardware comparisons.
- Investigate phase-sensitive quantum-state estimation.
- Build an interactive Streamlit dashboard for quantum fractal exploration.

## License

No license has been specified for this project. Add an appropriate license file before distributing the project under explicit reuse terms.
