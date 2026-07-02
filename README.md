# Pandana Update Test

Quick test of a local `pandana` build against sample network/household data.

The `pandana` package published on PyPI ships C++ extensions precompiled against NumPy 1.x. NumPy 2.0 changed its C API/ABI, so those precompiled binaries aren't compatible with a NumPy 2.0+ environment. This repo instead points at the `jkolberg/pandana` fork's `pandas_23` branch (updated for NumPy 2.0+ / pybind11 2.12+) and forces a local source build (`no-binary-package = ["pandana"]` in `pyproject.toml`) so the C++ extension gets recompiled against the newer NumPy headers/ABI instead of using the stale PyPI wheel.

## Setup

1. **(Windows only) Install the [Microsoft Visual C++ Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)** — required to run the compiled `pandana` C++ extension. Download and install the latest `x64` version from that page (macOS / Linux can skip this step).

2. **Install [uv](https://docs.astral.sh/uv/getting-started/installation/)**:

   Windows (PowerShell):
   ```powershell
   powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
   ```

   macOS / Linux:
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

3. **Clone the `jkolberg/pandana` fork** (branch `pandas_23`) to a folder outside this repo:

   Windows (PowerShell):
   ```powershell
   git clone --branch pandas_23 https://github.com/jkolberg/pandana.git $HOME\UDST_forks\pandana
   ```

   macOS / Linux:
   ```bash
   git clone --branch pandas_23 https://github.com/jkolberg/pandana.git ~/UDST_forks/pandana
   ```

4. **Point `pyproject.toml` at the local clone** — update the path under `[tool.uv.sources]` to match where you cloned it:

   Windows:
   ```toml
   [tool.uv.sources]
   pandana = { path = "C:/Users/<you>/UDST_forks/pandana", editable = true }
   ```

   macOS / Linux:
   ```toml
   [tool.uv.sources]
   pandana = { path = "/home/<you>/UDST_forks/pandana", editable = true }
   ```

5. **Install dependencies**:
   ```bash
   uv sync
   ```
   Note: this will take awhile the first time you run uv sync because it has to compile the C components.

6. Open `pandana_test.ipynb` jupyter notebook and select the `pandana-update-test` kernel.