# QAOA Optimization Best Practices Workshop

A comprehensive workshop and toolkit for Quantum Approximate Optimization Algorithm (QAOA) with best practices for quantum computing on real hardware.

## 📁 Project Structure

```
opt-best-practices-workshop/
├── postprocessing/                # QAOA analysis and postprocessing tools
│   ├── qaoa_tools/               # Modular utilities package
│   │   ├── __init__.py           # Package initialization
│   │   ├── utils_general.py      # Core utilities and data structures
│   │   ├── postprocessor_greedy.py  # Greedy one-flip postprocessor
│   │   ├── postprocessor_mqc.py  # MQC-style multi-qubit correction
│   │   ├── visualization.py      # Plotting and visualization
│   │   ├── analysis.py           # End-to-end analysis workflow
│   │   ├── requirements.txt      # Package dependencies
│   │   └── README.md             # Detailed module documentation
│   ├── postprocessing_KK.ipynb   # Main analysis notebook
│   ├── utils_postprocessing_KK.py # Legacy utilities (deprecated)
│   └── Postprocessing_23Apr.pdf  # Documentation
├── .gitignore
├── LICENSE
└── README.md                      # This file
```

## 🚀 Quick Start

### Installation

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd opt-best-practices-workshop
   ```

2. **Install dependencies:**
   ```bash
   cd postprocessing/qaoa_tools/
   pip install -r requirements.txt
   ```

3. **Set up IBM Quantum credentials:**
   ```bash
   export QISKIT_IBM_TOKEN="your_token_here"
   export QISKIT_IBM_INSTANCE="your_instance_here"
   ```

### Running the Notebook

```bash
cd postprocessing/
jupyter notebook postprocessing_KK.ipynb
```

### Using the Tools Programmatically

```python
from qaoa_tools import *

# Generate a problem graph
graph = generate_d_regular_graph(n=25, d=4, seed=7)

# Get classical baseline
classical_opt, _ = maxcut_exact_ilp(graph)

# Run QAOA and analyze results
report = analyze_and_report(
    outdir=output_dir,
    config=config,
    graph=graph,
    backend_name=backend_name,
    circuits=circuits,
    artifacts=artifacts,
    classical_opt=classical_opt,
)
```

## 📚 Documentation

### QAOA Tools Package (`postprocessing/qaoa_tools/`)

A modular toolkit for QAOA analysis with:

- **Core Utilities** (`utils_general.py`): Graph operations, classical baselines, backend management, SAT mapping, circuit building, distribution analysis
- **Postprocessing Methods**: Greedy one-flip and MQC-style multi-qubit correction
- **Visualization** (`visualization.py`): Comprehensive plotting functions
- **Analysis Pipeline** (`analysis.py`): End-to-end workflow orchestration

See [`postprocessing/qaoa_tools/README.md`](postprocessing/qaoa_tools/README.md) for detailed documentation.

### Key Features

#### 1. **Modular Architecture**
- Clean separation of concerns
- Easy to extend and customize
- Reusable components

#### 2. **Comprehensive Analysis**
- Raw distribution statistics
- Post-selection filtering
- Multiple postprocessing methods
- Detailed visualizations

#### 3. **Flexible Configuration**
- Hardware or simulator execution
- Multiple backend options
- Configurable postprocessing pipeline
- Customizable output

#### 4. **Production Ready**
- Type hints throughout
- Comprehensive documentation
- Error handling
- Logging and progress tracking

## 🔧 Configuration

Example configuration:

```python
CONFIG = {
    # Backend
    "USE_REAL_BACKEND": True,
    "RUN_MODE": "hardware",  # or "simulator"
    "BACKEND_NAME": "ibm_marrakesh",
    
    # Problem
    "GRAPH_N": 25,
    "GRAPH_D": 4,
    "GRAPH_SEED": 7,
    
    # QAOA
    "REPS": 1,
    "SEED": 7,
    "SHOTS": 20000,
    
    # Postprocessing
    "POSTPROCESSORS": [
        HighProbGreedy1Flip(),
        MQCStyleMultiQubitCorrection(top_m=500, max_passes=3),
    ],
    
    # Output
    "PLOT_TOPK": 40,
    "SAVE_DIR": "qaoa_runs",
}
```

## 📊 Output

The analysis generates organized outputs:

```
output_directory/
├── plots/              # Visualizations (graphs, circuits, distributions)
├── tables/             # CSV and HTML tables with metrics
└── data/               # JSON files with raw and processed data
```

## 🎯 Use Cases

### 1. **Research and Development**
- Test different QAOA configurations
- Compare postprocessing methods
- Analyze quantum vs classical performance

### 2. **Education and Workshops**
- Learn QAOA best practices
- Understand quantum error mitigation
- Explore real hardware execution

### 3. **Production Workflows**
- Modular components for custom pipelines
- Comprehensive logging and reporting
- Flexible configuration system

## 🔬 Postprocessing Methods

### Greedy One-Flip
- **Reference**: Chancellor 2017
- **Method**: Applies greedy local search to improve solutions
- **Use Case**: Quick improvement with low computational overhead

### MQC-Style Multi-Qubit Correction
- **Reference**: Ayanzadeh et al. Sci Rep 11, 16119 (2021)
- **Method**: Uses reference solutions to identify and correct groups of qubits
- **Use Case**: More sophisticated error mitigation for better results

## 🤝 Contributing

Contributions are welcome! Please:
1. Use the modular structure in `postprocessing/qaoa_tools/`
2. Maintain backward compatibility
3. Add tests for new features
4. Update documentation

## 📄 License

See [LICENSE](LICENSE) file for details.

## Acknowledgments

- IBM Quantum for hardware access
- Qiskit community for tools and support
- Research papers:
  - Chancellor 2017: Hybrid local search methods
  - Ayanzadeh et al. 2021: Multi-qubit correction

## 📧 Support

For questions or issues:
1. Check the documentation in `postprocessing/qaoa_tools/README.md`
2. Review the notebook in `postprocessing/postprocessing_KK.ipynb`
3. Refer to the PDF documentation
