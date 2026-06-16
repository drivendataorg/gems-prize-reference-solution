# Reference solution for the GEMS Prize Challenge

**Author**: Professor [John Lipor](https://web.cecs.pdx.edu/~lipor/)

This repository contains a reference solution for the GEMS Prize Challenge. The benchmark is implemented in Python and uses standard libraries to provide a baseline for comparison with other solutions.

## Getting started

1. Clone the repository:

   ```bash
   git clone https://github.com/drivendataorg/gems-prize-reference-solution
   cd gems-prize-reference-solution
   ```

2. Download the data from the GEMS Prize Challenge website and place it in the `data/` directory.

3. Set up the environment. Use whichever package manager you prefer. Each comes in a
   **GPU** and a **CPU-only** flavor — pick one based on your hardware (see
   [Choosing GPU vs. CPU](#choosing-gpu-vs-cpu) below).

   **Option A — [uv](https://docs.astral.sh/uv/getting-started/installation/) (recommended):**

   ```bash
   uv sync --locked --extra cu126   # NVIDIA GPU, CUDA 12.6
   uv sync --locked --extra cu130   # NVIDIA GPU, CUDA 13.0
   uv sync --locked --extra cpu     # CPU-only (and Apple Silicon / MPS)
   ```

   **Option B — conda:**

   ```bash
   conda env create -f environment.yml       # GPU where available (CUDA or Apple MPS)
   conda env create -f environment-cpu.yml   # CPU-only
   conda activate gems-prize-reference-solution
   ```

4. Run a notebook server and open `unet-mc-cv-reference-solution.ipynb`:

   ```bash
   uv run jupyter lab    # uv
   jupyter lab           # conda (after activating the environment)
   ```

## Choosing GPU vs. CPU

Training is much faster on a GPU, so use one if you have it.

- **NVIDIA GPU:** Pick the option matching your installed CUDA driver. CUDA 12.6
  (`cu126`) has the widest driver support; CUDA 13.0 (`cu130`) needs newer drivers.
  With conda, `environment.yml` selects a CUDA build automatically; pin a specific
  version by uncommenting a `cuda-version` line in that file.
- **Apple Silicon (M-series) Mac:** Use the `cpu` option for uv or `environment.yml`
  for conda. The standard macOS PyTorch build includes the Metal (MPS) GPU backend —
  there are no separate "Mac GPU" wheels. The notebook automatically uses MPS when
  available (it tries `cuda`, then `mps`, then `cpu`).
- **No GPU:** Use the `cpu` option (uv) or `environment-cpu.yml` (conda) for the
  smallest install.
