# Genome Assembly via De Bruijn Graphs

An algorithmic, from-scratch implementation of a **De Bruijn Graph Genome Assembler** written in Python. This tool builds a custom directed graph from short DNA reads and performs graph traversal to find a Eulerian path, reconstructing the original genome template.

## Project Purpose
Next-Generation Sequencing (NGS) produces millions of short, overlapping reads. Reconstructing the original genome from these reads is a core computational biology problem. This project implements a **De Bruijn Graph Assembler** that:
* Generates overlapping $k$-mers from a set of reads.
* Automatically includes reverse complement reads to handle double-stranded DNA sequencing.
* Models the assembly problem as a graph-based search for a Eulerian path/cycle.
* Dynamically identifies the optimal $k$ value required to successfully resolve and assemble the complete genome.

## Key Algorithmic Implementations
The sequence assembly logic is implemented from scratch using basic Python data structures:
1. **Reverse Complement Generation (`rc`)**: Computes the reverse complement of a DNA read using a base-mapping dictionary and slicing, which ensures coverage of both strands of a DNA molecule.
2. **K-mer Generation (`getkmers`)**: Slices DNA sequences into overlapping subsequences of length $k$ to represent them as nodes in the graph.
3. **De Bruijn Graph Construction (`DeBruijn`)**: Builds a directed graph represented as an adjacency-list dictionary:
   $$\text{Graph}[k\text{-mer prefix}] = [k\text{-mer suffix}_1, k\text{-mer suffix}_2, \dots]$$
   where the prefix of length $(k-1)$ links to the suffix of length $(k-1)$.
4. **Eulerian Assembly Solver (`genomeAssembly`)**: 
   * Iterates $k$-mer sizes from read length $L-1$ down to 2.
   * Constructs the global graph from reads and their reverse complements.
   * Traverses the graph by removing visited edges (following a Eulerian path) until returning to the start node.
   * Reconstructs and returns the final assembled genome, the optimal $k$ used, and the total genome length.

## Technologies Used
* **Python 3**
* **Jupyter Notebook** (development/execution environment)

## Prerequisites
Ensure Python 3 and Jupyter Notebook are installed on your machine.
Install Jupyter Notebook if needed:
```bash
pip install notebook
```

## Input File Format (`reads_lab6.txt`)
The input is a text file containing raw, single-line DNA read sequences:
```text
GCACTGCCAGACCGTGTTATGGCATCTGGTCAATAACCGGAACGGCCTAG
GAACGGCCTAGGGTTTCATCTCTGTTTGAGATCGATTTAGAGGTCGGAAC
CTCCTCGTTCCCTAACACATATTATCTGGGCGCCCCGGAACCCTCCTTTT
...
```

## How to Run
1. Open the Jupyter Notebook:
   ```bash
   jupyter notebook BIO310-Lab6code-EkinRenasKatirci.ipynb
   ```
2. Upload the `reads_lab6.txt` input file to the workspace.
3. Execute the notebook cells sequentially to compile the functions and run the assembler.
4. The notebook will automatically output the assembled genome string, the $k$ size used, and the total length of the sequence.

### Example Assembly Output
```python
# Output format: (Genome String, k-mer size, Genome Length)
('TGCAAACCGCACAGAATAGA...', 37, 2000)
```

